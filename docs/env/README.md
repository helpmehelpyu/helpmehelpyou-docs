# Environment Variables

## List of Environment Variables

| Name                  | Description                                       |
| --------------------- | ------------------------------------------------- |
| PORT                  | The port where the server is running              |
| POSTGRES_USERNAME     | The username to connect to the postgres db        |
| POSTGRES_HOST         | The hostname of the postgres db                   |
| POSTGRES_DATABASE     | The database of the postgres db                   |
| POSTGRES_PORT         | The port of the postgres db                       |
| POSTGRES_PASSWORD     | The password to connect to the postgres db        |
| POSTGRES_SSL_REQUIRED | Sets the SSL option to connect to the postgres db |

## Example .env file for develpment

```.env
PORT=3000
POSTGRES_USERNAME=postgres
POSTGRES_HOST=db
POSTGRES_DATABASE=postgres
POSTGRES_PORT=5432
POSTGRES_PASSWORD=password
POSTGRES_SSL_REQUIRED=false
```

This is the one I use locally. Ideally you don't use the production db on Heroku for development. The credentials for the production db can change so make sure to check the [credentials](https://data.heroku.com/datastores/583b4ec1-bf79-4560-a22a-ce251b920312#administration) before you use it.

Yes the password is password.
