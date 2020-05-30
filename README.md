# REST APIs with Flask
以 Flask 建立符合 REST 風格的 API 伺服器應用程式。

## Basics
內容源自於 Udemy 的 "[REST APIs with Flask and Python](https://www.udemy.com/course/rest-api-flask-and-python/)" 線上課程。

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

## Advanced
內容源自於 Udemy "[Advanced REST APIs with Flask and Python](https://www.udemy.com/course/advanced-rest-apis-flask-python)" 線上課程。
