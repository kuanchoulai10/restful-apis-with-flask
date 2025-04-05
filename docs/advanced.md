# Advanced

## Section 1: Course Preparations
Preparations for the course:

- Simplified authentication mechanism.
- Added type hinting.
- Unified code style.
- Changed all `Resource` methods to class methods (using `@classmethod`).

## Section 2: Marshmallow Integration
Introducing [`marshmallow`](https://pypi.org/project/marshmallow/), [`flask-marshmallow`](https://pypi.org/project/flask-marshmallow/), and [`marshmallow-sqlalchemy`](https://pypi.org/project/marshmallow-sqlalchemy/):

- Simplified request parsing, `Model` object creation, and JSON responses by defining `Schema` for each `Resource`.

## Section 3: Email Verification
- Implemented user email verification process (using [Mailgun](https://www.mailgun.com/)).
- Used `.env` files to store sensitive data.
- Returned `.html` files in [`Flask-RESTful`](https://pypi.org/project/Flask-RESTful/) using `make_response()` and `render_template()`.

## Section 4: Optimized Email Verification
Optimized the email verification process:

- Added expiration for verification and resend functionality.
- Refactored project structure by treating `confirmation` as a resource.

## Section 6: Secure Configuration and File Uploads
- Configured the application more securely (using `from_object()` and `from_envvar()`).
- Learned the relationships between `WSGI`, `uwsgi`, `uWSGI`, and `Werkzeug`.
- Introduced [`Flask-Uploads`](https://pypi.org/project/Flask-Uploads/) for handling file uploads, downloads, and deletions (using `UploadSet`, `FileStorage`).

## Section 7: Database Version Control
- Introduced [`Flask-Migrate`](https://pypi.org/project/Flask-Migrate/) for database version control, including adding, deleting, and modifying details.
- Common commands include `flask db init`, `flask db upgrade`, `flask db downgrade`.

## Section 8: OAuth Integration
- Learned OAuth third-party login flow (e.g., GitHub), including authentication, authorization, and obtaining `access_token`.
- Introduced [`Flask-OAuthlib`](https://pypi.org/project/Flask-OAuthlib/).
- Used Flask's `g` to store `access_token`.
- Allowed third-party login users to set passwords.

## Section 9: Payment Integration
- Integrated `Stripe` for third-party payment processing.
- Added an "Order" resource and implemented many-to-many relationships using `Flask-SQLAlchemy`.
