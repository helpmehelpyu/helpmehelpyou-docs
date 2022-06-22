# Database Setup

## Creating the local database

If you already created a database omit this step.

In order to set up the database, we must first create the database.

Firstly, connect to the database with

```bash
psql -h localhost -p 5432 -U postgres
```

Then you can create a database with

```bash
CREATE DATABASE <database_name>
```

After running this command the terminal should check CREATE DATABASE, and if you type `\l` you should see your database in the list. Now you've set up the local database, and should only do this step again when you delete the database.

# Setting Up the Tables

In order to set up the local postgres-docker database tables simply run

```bash
npm run typeorm migration:run -- -d ./database/dataSource.ts
```

This will run all migrations and set up the database.

Make sure that you are connected to the database.

## Generating Migrations

A migration is effectivly a database commit. When you run the migration you run the change on the database (i.e alter a table). When you revert the migration you revert the change. With [Typeorm](https://typeorm.io/migrations) we can generate migrations whenever we change the database which is pretty sweet. Then another user with the old database can simply run (the command above) the migration to synchronize their database.

First, connect to the docker container which is running the server (I have no clue how to do this without it).

Then run

```bash
npm run typeorm migration:generate -- ./database/migrations/<NAME_OF_MIGRATION> -d ./database/dataSource.ts
```

This will generate a migration named `NAME_OF_MIGRATION` concatenated with a timestamp in the `server/database/migrations` folder.

_BAM_ You have now generated a super cool database migration!.

## Running Migrations

Is the same process as initially setting up the database. Just navigate to the server folder (not in docker container) and run

```bash
npm run typeorm migration:run -- -d ./database/dataSource.ts
```
