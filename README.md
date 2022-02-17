## Using this as a template:
Fork this project to create a template. Then, clone this new project.

Run this to install all dependencies (which are listed in `package.json`). This will create the `node_modules` folder and `package-lock.json`

```
> npm install
```

Copy the file `.sample-env` and rename the copy `.env`. 
Add the configuration values for your database into `.env`:

You can run the server in one of two ways:
1. Standard server start (essentially runs `node ./bin/www`)
  ```
  > npm start
  ```
  This can be stopped with `Ctrl-C`.
2. Nodemon server start:
  ```
  > npm run devstart
  ```
  This should automatically restart the server upon changes to your files. Manually restart by typing `rs` in the Terminal; stop with `Ctrl-C`

## How was this built?


### Basic configuration
The app's skeleton structure was generated with:
```
> npx express-generator --view=hbs
```
In addition to installing the packages used by the skeleton structure, the `mysql` and `dotenv` packages were installed, and the `nodemon` package was installed as a development dependency:
```
> npm install
> npm install mysql dotenv
> npm install nodemon --save-dev
```

The `package.json` file's `scripts` section was manually updated with the line `"devstart": "nodemon -e js,hbs,css,env,sql ./bin/www"`. 

Now `package.json` looked something like this (version numbers may vary if you reproduce)

```json
{
  "name": "ib-webapp-template-express-hbs-mysql-materialize",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www",
    "devstart": "nodemon -e js,hbs,css,env,sql ./bin/www"
  },
  "dependencies": {
    "cookie-parser": "~1.4.4",
    "debug": "~2.6.9",
    "dotenv": "^16.0.0",
    "express": "~4.16.1",
    "hbs": "~4.0.4",
    "http-errors": "~1.6.3",
    "morgan": "~1.9.1",
    "mysql": "^2.18.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.15"
  }
}

```

A `.env` file (for defining values for environment variables) is added.

The `.env` was given the following content:
```
DB_DATABASE=
DB_HOST=
DB_USER=
DB_PASSWORD=
DB_PORT=3306
DB_CONNECT_TIMEOUT=10000
LOG_QUERY=True
LOG_QUERY_ARGS=True
LOG_QUERY_SUMMARY=True
LOG_QUERY_RESULTS=True
```
The values for sensitive database configuration information was also added to the `DB` environment variables.

A copy of `.env` called `.sample-env` was made without any sensitive values included. 

A folder called `db` was created, and the file called `db.js` was added, which is a local module for a MySQL database connection pool. 

To make git not track `node_modules` or `.env`, a `.gitignore` file was added with the following content:
```
node_modules
.env
```