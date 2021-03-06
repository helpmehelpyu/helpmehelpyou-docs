# Environment Variables

Setup instructions and documentation for .env file.

**THE `.env` FILE GOES IN THE `/server/config` FOLDER**

## List of Environment Variables

| Name              | Description                                          |
| ----------------- | ---------------------------------------------------- |
| PORT              | The port where the server is running                 |
| DATABASE_URL      | The url of the database which can be used to connect |
| POSTGRES_PASSWORD | The password of the local postgres db                |
| TOKEN_SECRET      | The secret used to hash passwords and generate salts |

## Example .env file for develpment

```.env
# sever
PORT=3000

# database
POSTGRES_PASSWORD=password
DATABASE_URL=postgresql://postgres:password@db:5432/postgres

# SECRET
TOKEN_SECRET=secret
```

This is the one I use locally. Ideally you don't use the production db on Heroku for development. The credentials for the production db can change so make sure to check the [credentials](https://data.heroku.com/datastores/583b4ec1-bf79-4560-a22a-ce251b920312#administration) before you use it.

Yes the password is password.
