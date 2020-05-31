# 將 Flask 應用程式部署在 Ubuntu 16.04 Server
首先，我們必須註冊 DigitalOcean 帳號並在上面租用一個虛擬主機，版本為 Ubuntu 16.04 Server。如何以 SSH 連線不是課程重點，因此我們在此先略過。連線後緊接著進行幾項事前準備：

### 更新倉庫清單
```
# apt-get update
```

### 在 OS 上創建新使用者
```
# adduser <username>
```

### 給予 super user 權限
進入 `/etc/sudoers` 檔案：
```
# visudo
```

在 "User privilege specification" 下方替新使用者加入 super user 的權限：
```
<username> ALL=(ALL:ALL) ALL
```

## 1. 安裝並設定 PostreSQL 資料庫
### 安裝 PostgreSQL
```
# apt-get install postgresql postgresql-contrib
```

### 切換成 `postgres` 使用者
```
# sudo -i -u postgres
```

### 替新使用者，創建 PostgreSQL 當中的帳號和資料庫
```
$ createuser <username> -P
$ createdb <username>
```

### 強制以密碼登入 PostgreSQL
進入 `pg_hba.conf` 配置檔：
```
$ nano /etc/postgresql/10/main/pg_hba.conf
```

將
```
local all all peer
```
改為
```
local all all md5
```

完成後跳出配置檔，接著改為新使用者來操作。


## 2. 安裝並設定 Nginx 伺服器
### 安裝 Nginx
```
$ sudo apt-get install nginx
```
### 開啟防火牆並允許 `nginx` 和 `ssh`
```
$ sudo ufw enable
$ sudo ufw allow 'Nginx HTTP'
$ sudo ufw allow ssh
```

### 替我們的 Flask 應用程式加入 Nginx 配置檔
創建並進入 `items-rest.conf` 配置檔：
```
$ sudo nano /etc/nginx/sites-available/items-rest.conf
```

輸入以下內容：
```
server {
	listen 80;
	real_ip_header X-Forwarded-For;
	set_real_ip_from 127.0.0.1;
	server_name localhost;

	location / {
		include uwsgi_params;
		uwsgi_pass unix:/var/www/html/items-rest/socket.sock;
		uwsgi_modifier1 30;
	}

	error_page 404 /404.html;
	location = 404.html {
		root /usr/share/nginx/html;
	}

	error_page 500 502  503 504 50x.html;
	location = /50x.html {
		root /usr/share/nginx/html;
	}
}
```

完成後跳出配置檔，接著建立 soft link，啟用配置：
```
$ sudo ln -s /etc/nginx/sites-available/items-rest.conf /etc/nginx/sites-enabled/
```

## 3. 設定 Flask 應用程式所需執行環境
### 創建專案目錄並給予適當權限
```
$ sudo mkdir /var/www/html/items-rest
$ sudo chown <username>:<username> /var/www/html/items-rest
```

完成後進入該目錄：
```
$ cd /var/www/html/items-rest
```

### 設定專案所需環境
下載專案內容並創建日誌檔目錄：
```
$ git clone https://github.com/schoolofcode-me/stores-rest-api.git .
$ mkdir log
```

建立虛擬環境並安裝所需套件：
```
$ sudo apt-get install python-pip python3-dev libpq-dev
$ pip install virtualenv
$ virtualenv venv --python=python3.6
$ source venv/bin/activate
(venv)$ pip install -r requirements.txt
```

# 4. 設定 uWSGI 伺服器
### 創建 `uwsgi_items_rest.service` Ubuntu 服務
創建並進入 `uwsgi_items_rest.service` 檔：
```
$ sudo nano /etc/systemd/system/uwsgi_items_rest.service
```

輸入以下內容：
```
[Unit]
Description=uWSGI items rest

[Service]
Environment=DATABASE_URL=postgres://jose:1234@localhost:5432/jose
ExecStart=/var/www/html/items-rest/venv/bin/uwsgi --master --emperor /var/www/html/items-rest/uwsgi.ini --die-on-term --uid jose --gid jose --logto /var/www/html/items-rest/log/emperor.log
Restart=always
KillSignal=SIGQUIT
Type=notify
NotifyAccess=all

[Install]
WantedBy=multi-user.target
```

完成後跳出檔案。

### 修改 `uwsgi.ini` 配置檔
進入專案內的 `uwsgi.ini` 配置檔：
```
$ nano uwsgi.ini
```

輸入以下內容：
```
[uwsgi]
base = /var/www/html/items-rest
app = run
module = %(app)

home = %(base)/venv
pythonpath = %(base)

socket = %(base)/socket.sock

chmod-socket = 777

processes = 8

threads = 8

harakiri = 15

callable = app

logto = /var/www/html/items-rest/log/%n.log
```

完成後跳出配置檔。

# 5. 啟動 Flask 應用程式
刪除 Nginx 預設配置檔，避免讀取錯誤的配置檔，接著 reload 並 restart：
```
$ sudo rm /etc/nginx/sites-enabled/default
$ sudo systemctl reload nginx 
$ sudo systemctl restart nginx
```

啟動 `uwsgi_items_rest` 服務：
```
$ sudo systemctl start uwsgi_items_rest
```

完成！
