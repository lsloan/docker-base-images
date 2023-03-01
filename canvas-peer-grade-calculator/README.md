# canvas-peer-grade-calculator - - README

This project is a deployment wrapper for Longhorn Open Ed Tech's [canvas-peer-grade-calculator](https://github.com/longhornopen/canvas-peer-grade-calculator).

Docker uses an image from the project's container package, [canvaspeergrade](https://github.com/longhornopen/canvas-peer-grade-calculator/pkgs/container/canvaspeergrade).

1. Copy `.env.sample` to `.env`…
    ```shell
    cp .env.sample .env
    ```
2. Edit `.env` contents, using the comments therein as a guide.  Additional
   information can be found in Longhorn's [README.md](https://github.com/longhornopen/canvas-peer-grade-calculator/blob/6a2ece08b61a16a28f57d841a0399ca99081cbf4/README.md)
   for their project.
3. Start the app and db containers with Docker `compose`…
    ```shell
    docker compose up --build
    ```
4. (Temporary) Run DB migrations.  
    The following DB migrations need to be applied manually until they can be
    added to the Docker process and be applied automatically.  These migrations
    should **_NOT_** be run multiple times with the same database.  The
    step for creating the session table migration will make **_ANOTHER_**
    migration, which will **_FAIL_** if it is applied again.
   * Create a migration for the session database table.  
     A migration for this was not included in the Docker image provided by
     Longhorn Open.
     ```shell
     docker compose exec app php artisan session:table
     ```
   * Run the database migrations.  
     Apply all the migrations to the DB.  At this time, there are four
     migrations.  Three included in the Docker image and one created in the
     previous step.
     ```shell
     docker compose exec app php artisan migrate
     ```
