# REST APIs with Flask
以 Flask 建立符合 REST 風格的 API 伺服器應用程式。

## Basics
[證書](https://www.udemy.com/certificate/UC-7fddb0fd-9c04-4579-86f5-7b9dda42f9b3/)，內容源自於 Udemy 的 "[REST APIs with Flask and Python](https://www.udemy.com/course/rest-api-flask-and-python/)" 線上課程。

### Section 3
- 初探 Flask 網頁框架，以 decorator 設定網頁應用程式的 route。
- 了解 GET, POST, PUT, DELETE 等常見的 HTTP 請求方法。
- 了解 200, 201, 202, 401, 404 等常見的 HTTP 狀態碼。
- 了解 RESTful API 設計需聚焦在「資源」(resource) 並且符合無狀態的(stateless)特性。
- 實作 RESTful API 伺服器應用程式。
- 以 Postman 應用程式進行 API 測試。

### Section 4
- 以 [`Flask-RESTful`](https://pypi.org/project/Flask-RESTful/) 實作 RESTful API 伺服器應用程式。
- 以 [`Flask-JWT`](https://pypi.org/project/Flask-JWT/) 實作 JSON Web Token (JWT) 使用者驗證機制。
- 使用 `RequestParser` 解析使用者輸入的 JSON 資料。

### Section 5
- 導入 `sqlite3`，改為從資料庫存取使用者和商品資訊。
- 實作使用者註冊機制。

### Section 6
- 導入 [`Flask-SQLAlchemy`](https://pypi.org/project/flask-sqlalchemy/)，以 ORM 機制操作資料庫。
- 加入商店資訊，與商品為一對多的關聯關係。

### Section 8
將 Flask 應用程式部署在 Heroku 上，並使用 Heroku 提供的 PostgresSQL，步驟：
1. 在本機端增修專案內容，如加入 `Procfile`, `runtime.txt`, `uwsgi.ini`等，接著 `commit` 並 `push` 至 GitHub 上的指定 repo。
2. 在 Heroku 官方網站註冊帳號，接著創建一個應用程式並與 GitHub 指定 repo 連線，再來加入 buildpack `heroku/python` 和 add-ons `Heroku Postgres`。
3. 在本機端安裝 Heroku CLI（參考[這裡](https://devcenter.heroku.com/articles/heroku-cli)）並透過 `heroku login` 指令登入 Heroku。
4. 在本機端透過 `heroku git:remote -a <app-name>` 指令，加入 Heroku 遠端節點。
5. 在本機端透過 `git subtree push --prefix basics/section8 heroku master` 指令，將當前專案內容的子目錄 `push` 至 Heroku 的遠端節點並部署上線。

測試：
連線至[這裡](http://rest-apis-with-flask.herokuapp.com/stores)，取得資料庫當中所有的商店及其商品，以 `JSON` 格式回傳。

### Section 9
將 Flask 應用程式部署在 DigitalOcean 提供的 Droplet 虛擬主機上，步驟：
1. 註冊 DigitalOcean 帳號並創建個 Droplet 虛擬主機，作業系統為 Ubuntu 16.04，接著設定 SSH 連線，在本機端使用 PuTTY 以 SSH 連線至遠端虛擬主機。
2. 在作業系統當中創建一個新的使用者。
3. 安裝並設定 PostgreSQL 資料庫，包括在 PostgreSQL 當中創建新使用者以及資料庫，並設定相關權限。
4. 安裝並設定 Nginx 伺服器，包括防火牆設定、錯誤頁面、uwsgi 參數等。
5. 設定 Python 虛擬環境，接著安裝專案所需套件，並把專案內容從 GitHub `clone` 下來。
6. 設定個 Ubuntu 服務，用來開啟 uwsgi 伺服器，負責執行我們的 Flask 應用程式，包括日誌檔儲存目錄、跑幾個程序、幾個執行緒等。

測試：
連線至[這裡](http://64.225.122.125/stores)（創建日期 2020/05/30），取得資料庫當中所有的商店及其商品，以 `JSON` 格式回傳。

### Section 10
[電子書](https://school-of-code.gitbooks.io/rest-apis-with-flask-and-python/content/domains-and-https/what-is-a-domain.html)
- 註冊域名、設定 DNS 伺服器。
- 取得 SSL 數位憑證，以 https 通訊協定連線，設置 Nginx。

### Section 11
導入 [`Flask-JWT-Extended`](https://pypi.org/project/Flask-JWT-Extended/)：
- 實作 token-refreshing 機制，提升用戶瀏覽體驗，不需要定期重新輸入帳號密碼，同時設定重要操作時仍需重新登入，提升安全性（使用 `@jwt_refresh_token_required`, `create_refresh_token()`, `create_access_token()` 等）。
- 針對各個權限的請求，如訪客、一般使用者、管理員，回應相對應的資料（使用 `@jwt.user_claims_loader`, `@jwt_optional`, `get_jwt_claims()` 等）。
- 針對各個權限錯誤的請求，回傳相對應的錯誤訊息（使用 `@jwt.expired_token_loader`, `@jwt.invalid_token_loader`, `@jwt.needs_fresh_token_loader` 等）。
- 以黑名單（blacklist）設定，實作登出機制（使用 `@jwt.token_in_blacklist_loader`, `get_raw_jwt()` 等）。

[電子書](https://arac.tecladocode.com/)


## Advance
內容源自於 Udemy "[Advanced REST APIs with Flask and Python](https://www.udemy.com/course/advanced-rest-apis-flask-python)" 線上課程。

### Section 1
為了接下來的課程內容，做了幾項事情準備：
- 簡化驗證機制。
- 加入 type hinting。
- 統一程式碼風格。
- 所有 `Resource` 的方法統一改為類別方法（使用 `@classmethod`）。

### Section 2
導入 [`marshmallow`](https://pypi.org/project/marshmallow/), [`flask-marshmallow`](https://pypi.org/project/flask-marshmallow/) 和 [`marshmallow-sqlalchemy`](https://pypi.org/project/marshmallow-sqlalchemy/)：
- 透過定義好每個 `Resource` 的 `Schema`，簡化「請求解析」、「創建 `Model` 物件」、「回傳 JSON」的過程。

### Section 3
- 實作使用者電子信箱認證流程（使用 [Mailgun](https://www.mailgun.com/) 服務）。
- 在專案中使用 `.env` 檔案儲存敏感資料。
- 在 [`Flask-RESTful`](https://pypi.org/project/Flask-RESTful/) 框架中回傳 `.html` 檔案（使用 `make_response()` 和 `render_template()`）。

### Section 4
優化使用者電子信箱認證流程：
- 有效認證期限、重傳認證信。
- 專案程式架構優化（抽出 `confirmation` 功能作為「資源」看待）。

### Section 6
- 以更安全的方式配置應用程式（使用 `from_object()` 和 `from_envvar()`等）。
- 瞭解 `WSGI`, `uwsgi`, `uWSGI`, `Werkzeug` 之間的關係。
- 導入 [`Flask-Uploads`](https://pypi.org/project/Flask-Uploads/)，實作圖片、大頭貼上傳、下載、刪除等功能（使用 `UploadSet`, `FileStorage`等）。

### Section 7
- 導入 [`Flask-Migrate`](https://pypi.org/project/Flask-Migrate/)，對資料庫進行版本控制，新增、刪除、修改其細節。
- 常見指令如 `flask db init`, `flask db upgrade`, `flask db downgrade`等。

### Section 8
- 了解 OAuth 第三方登入的流程（以 GitHub 為例），包括了認證和授權，取得 `access_token` 等。
- 導入 [`Flask-OAuthlib`](https://pypi.org/project/Flask-OAuthlib/)。
- 使用 `Flask` 的 `g` 來儲存 `access_token`。
- 允許使用第三方登入的使用者設定密碼。
