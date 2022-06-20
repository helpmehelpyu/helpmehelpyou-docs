# Getting Started with the Server

First navigate to the [server folder](https://github.com/helpmehelpyu/helpmehelpyou/tree/main/server) with your terminal of choice (there was never really a choice, use [zsh](https://github.com/ohmyzsh/ohmyzsh 'bash is also acceptable but its not as cool')).

## Start Server with Local Postgres server

In order to start a local server with a local postgres server run:

```bash
npm run dev
```

**[Make sure to set the .env file before you attempt to run the docker images](/env/)**

This will first build two [Docker](https://docs.docker.com/) images, one for the server and one for the database.
Then it will run the images in two containers.

The server will be accessible at [localhost:3000](http://localhost:3000) and the postgres db should be available at the ip address 0.0.0.0, port 5432. The password, username, etc for the db can be found in the [.env file](/env/).

You can connect to the db with the command

```bash
psql -h localhost -p 5432 -U postgres
```

I have no idea how to connect to it with [pgAdmin](https://www.pgadmin.org/), so if anyone figures that out let me know. For now I will live on the command line.

Hot reloading is also set up.

## Install

In order to install dependencies, simply run:

```bash
npm install
```

## Build

To build the server run:

```bash
npm run build
```

---

#### **NOTE: Make sure to build before you try to start the server for the first time**

---

## Start Server for Production

To Start the server for Production, i.e. no hot reloading

```bash
npm run start
```

## Start Server for Development (hot reloading)

To start the server (only server not local postgres db as well) for Development just run

```bash
npm run dev-server
```

whenever you save your work, the server should update to reflect your new changes. Some changes require the server to be restarted manually. That is, kill the server with `Ctrl-C`, then restart again.
