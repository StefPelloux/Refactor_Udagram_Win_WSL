



# From : https://www.youtube.com/watch?v=EJMp1IINGdU&ab_channel=ScalpAcademy



### Prerequisite Intalled on Windows 11/ WSL2

 wsl -l -v
  NAME                   STATE           VERSION
* ubuntu20-04            Running         2


1. The depends on the Node Package Manager (NPM). You will need to download and install Node from [https://nodejs.com/en/download](https://nodejs.org/en/download/). This will allow you to be able to run `npm` commands.
2. Environment variables will need to be set. These environment variables include database connection details that should not be hard-coded into the application code.

npm -v
6.14.18
node -v
v14.21.3

ionic --v
   _             _
  (_) ___  _ __ (_) ___
  | |/ _ \| '_ \| |/ __|
  | | (_) | | | | | (__
  |_|\___/|_| |_|_|\___| CLI 5.4.16


### 1. Database
Create a PostgreSQL database either locally or on AWS RDS. The database is used to store the application's metadata.

* We will need to use password authentication for this project. This means that a username and password is needed to authenticate and access the database.
* The port number will need to be set as `5432`. This is the typical port that is used by PostgreSQL so it is usually set to this port by default.

Once your database is set up, set the config values for environment variables prefixed with `POSTGRES_` in `set_env.sh`.
* If you set up a local database, your `POSTGRES_HOST` is most likely `localhost`
* If you set up an RDS database, your `POSTGRES_HOST` is most likely in the following format: `***.****.us-west-1.rds.amazonaws.com`. You can find this value in the AWS console's RDS dashboard.


sudo apt install postgresql postgresql-contrib
sudo service postgresql start


netstat -an | grep 5432
tcp        0      0 172.17.0.1:5432         0.0.0.0:*               LISTEN



/etc/postgresql/12/main/pg_hba.conf
host    all             all             0.0.0.0/0               md5



sudo su - postgres
psql
ALTER USER postgres WITH PASSWORD 'petitponey';






### 2. S3
Create an AWS S3 bucket. The S3 bucket is used to store images that are displayed in Udagram.

Set the config values for environment variables prefixed with `AWS_` in `set_env.sh`.


#### Environment Script
A file named `set_env.sh` has been prepared as an optional tool to help you configure these variables on your local development environment.
source ../set_env.sh






### 3. Backend API
Launch the backend API locally. The API is the application's interface to S3 and the database.

* To download all the package dependencies, run the command from the directory `udagram-api/`:
    ```bash
    npm install .
    ```
* To run the application locally, run:
    ```bash
    npm run dev
    ```

#  Exemple -------------------

# [INFO] 14:14:45 ts-node-dev ver. 1.1.8 (using ts-node ver. 9.1.1, typescript ver. 3.9.10)
# Initialize database connection...
# (node:2273) NOTE: We are formalizing our plans to enter AWS SDK for JavaScript (v2) into maintenance mode in 2023.
# 
# Please migrate your code to use AWS SDK for JavaScript (v3).
# For more information, check the migration guide at https://a.co/7PzMCcy
# (Use `node --trace-warnings ...` to show where the warning was created)
# Executing (default): CREATE TABLE IF NOT EXISTS "FeedItem" ("id"   SERIAL , "caption" VARCHAR(255), "url" VARCHAR(255), "createdAt" TIMESTAMP WITH TIME ZONE, "updatedAt" TIMESTAMP WITH # TIME ZONE, PRIMARY KEY ("id"));
# Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS # column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'FeedItem' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
# Executing (default): CREATE TABLE IF NOT EXISTS "User" ("email" VARCHAR(255) , "passwordHash" VARCHAR(255), "createdAt" TIMESTAMP WITH TIME ZONE, "updatedAt" TIMESTAMP WITH TIME ZONE, PRIMARY KEY ("email"));
# Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'User' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
# server running http://localhost:8100
# press CTRL+C to stop server



* You can visit `http://localhost:8080/api/v0/feed` in your web browser to verify that the application is running. You should see a JSON payload. Feel free to play around with Postman to test the API's.







### 4. Frontend App
Launch the frontend app locally.

* To download all the package dependencies, run the command from the directory `udagram-frontend/`:
    ```bash
    npm install .
    ```
* Install Ionic Framework's Command Line tools for us to build and run the application:
    ```bash
    npm install -g ionic
    ```
* Prepare your application by compiling them into static files.
    ```bash
    ionic build
    ```
* Run the application locally using files created from the `ionic build` command.
    ```bash
    ionic serve (2Mins for start)
    ```

####   ng run app:serve --host=localhost --port=8100
####  [INFO] Waiting for connectivity with ng...
####  [INFO] Waiting for connectivity with ng...
####  [INFO] Waiting for connectivity with ng...
####  [INFO] Waiting for connectivity with ng...
####  [INFO] Waiting for connectivity with ng...
####  [INFO] Waiting for connectivity with ng...
####  
####  [INFO] Development server running!
####  
####         Local: http://localhost:8100
####  
####  Use Ctrl+C to quit this process
####  
####  [INFO] Browser window opened to http://localhost:8100!
####  
####  [ng] ℹ ｢wdm｣: wait until bundle finished: /
####  [ng] Date: 2024-02-05T14:14:12.263Z
####  [ng] Hash: d0d8ddf1295d6fe8a85a
####  [ng] Time: 100354ms
####  [ng] chunk {common} common.js, common.js.map (common) 14.7 kB  [rendered]
####  [ng] chunk {es2015-polyfills} es2015-polyfills.js, es2015-polyfills.js.map (es2015-polyfills) 285 kB [initial] [rendered]
####  [ng] chunk {home-home-module} home-home-module.js, home-home-module.js.map (home-home-module) 31.4 kB  [rendered]
####  [ng] chunk {main} main.js, main.js.map (main) 64.8 kB [initial] [rendered]
####  [ng] chunk {polyfills} polyfills.js, polyfills.js.map (polyfills) 237 kB [initial] [rendered]
####  [ng] chunk {runtime} runtime.js, runtime.js.map (runtime) 8.79 kB [entry] [rendered]
####  [ng] chunk {styles} styles.js, styles.js.map (styles) 102 kB [initial] [rendered]
####  [ng] chunk {vendor} vendor.js, vendor.js.map (vendor) 4.71 MB [initial] [rendered]
####  [INFO] ... and 94 additional chunks
####  [ng] ℹ ｢wdm｣: Compiled successfully.















## Tips
1. Take a look at `udagram-api` -- does it look like we can divide it into two modules to be deployed as separate microservices?
2. The `.dockerignore` file is included for your convenience to not copy `node_modules`. Copying this over into a Docker container might cause issues if your local environment is a different operating system than the Docker image (ex. Windows or MacOS vs. Linux).
3. It's useful to "lint" your code so that changes in the codebase adhere to a coding standard. This helps alleviate issues when developers use different styles of coding. `eslint` has been set up for TypeScript in the codebase for you. To lint your code, run the following:
    ```bash
    npx eslint --ext .js,.ts src/
    ```
    To have your code fixed automatically, run
    ```bash
    npx eslint --ext .js,.ts src/ --fix
    ```
4. `set_env.sh` is really for your backend application. Frontend applications have a different notion of how to store configurations. Configurations for the application endpoints can be configured inside of the `environments/environment.*ts` files.
5. In `set_env.sh`, environment variables are set with `export $VAR=value`. Setting it this way is not permanent; every time you open a new terminal, you will have to run `set_env.sh` to reconfigure your environment variables. To verify if your environment variable is set, you can check the variable with a command like `echo $POSTGRES_USERNAME`.
