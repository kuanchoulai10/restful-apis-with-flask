# Flask Basics

## Section 3: Introduction to Flask
- Introduction to the Flask web framework, using decorators to set up application routes.
- Understanding common HTTP request methods: GET, POST, PUT, DELETE.
- Understanding common HTTP status codes: 200, 201, 202, 401, 404.
- Understanding RESTful API design principles focusing on "resources" and statelessness.
- Implementing a RESTful API server application.
- Testing APIs using the Postman application.

## Section 4: Flask-RESTful and JWT
- Implementing RESTful API server applications using [`Flask-RESTful`](https://pypi.org/project/Flask-RESTful/).
- Implementing JSON Web Token (JWT) authentication using [`Flask-JWT`](https://pypi.org/project/Flask-JWT/).
- Parsing user input JSON data using `RequestParser`.

## Section 5: Database Integration with SQLite
- Introducing `sqlite3` to store user and item information in a database.
- Implementing user registration functionality.

## Section 6: Database Integration with SQLAlchemy
- Introducing [`Flask-SQLAlchemy`](https://pypi.org/project/flask-sqlalchemy/) to interact with the database using ORM.
- Adding store information with a one-to-many relationship to items.

## Section 7: Deploying to Heroku
Deploying the Flask application to Heroku and using Heroku's PostgreSQL. Steps:

1. Modify the project locally (e.g., add `Procfile`, `runtime.txt`, `uwsgi.ini`), then `commit` and `push` to the specified GitHub repo.
2. Register on Heroku, create an application, connect it to the GitHub repo, and add the `heroku/python` buildpack and `Heroku Postgres` add-on.
3. Install the Heroku CLI locally (see [here](https://devcenter.heroku.com/articles/heroku-cli)) and log in using `heroku login`.
4. Add a Heroku remote using `heroku git:remote -a <app-name>`.
5. Deploy the project by pushing the `basics/section8` subdirectory to Heroku using `git subtree push --prefix basics/section8 heroku master`.

Testing:
Access [here](http://rest-apis-with-flask.herokuapp.com/stores) to retrieve all stores and their items in the database, returned in JSON format.

## Section 8: Deploying to DigitalOcean
Deploying the Flask application to a DigitalOcean Droplet. Steps:

1. Register on DigitalOcean, create a Droplet with Ubuntu 16.04, set up SSH, and connect using PuTTY.
2. Create a new user on the operating system.
3. Install and configure PostgreSQL, including creating a new user and database with appropriate permissions.
4. Install and configure the Nginx server, including firewall settings, error pages, and uwsgi parameters.
5. Set up a Python virtual environment, install required packages, and clone the project from GitHub.
6. Configure an Ubuntu service to run the uwsgi server, including log directories, processes, and threads.

Testing:
Access [here](http://64.225.122.125/stores) (created on 2020/05/30) to retrieve all stores and their items in the database, returned in JSON format.

## Section 9: Domain and HTTPS
[Book](https://school-of-code.gitbooks.io/rest-apis-with-flask-and-python/content/domains-and-https/what-is-a-domain.html)

- Registering a domain and configuring DNS servers.
- Obtaining an SSL certificate for HTTPS communication and configuring Nginx.

## Section 11: Advanced JWT Features
Introducing [`Flask-JWT-Extended`](https://pypi.org/project/Flask-JWT-Extended/):

- Implementing token-refreshing to improve user experience by avoiding frequent logins while requiring re-login for critical actions for security (using `@jwt_refresh_token_required`, `create_refresh_token()`, `create_access_token()`).
- Responding with appropriate data based on user roles (visitor, user, admin) using `@jwt.user_claims_loader`, `@jwt_optional`, `get_jwt_claims()`.
- Returning specific error messages for token-related issues using `@jwt.expired_token_loader`, `@jwt.invalid_token_loader`, `@jwt.needs_fresh_token_loader`.
- Implementing a logout mechanism using a blacklist (with `@jwt.token_in_blacklist_loader`, `get_raw_jwt()`).

[Book](https://arac.tecladocode.com/)
