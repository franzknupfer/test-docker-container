## Description

This is a basic scaffolded Rails project using Docker with Ruby 2.6.5, Rails 5.2.4, and Postgres 12.1. This project can be used in lieu of installing Ruby, Rails and Postgres on your machine. When you run `docker-compose up`, Docker will create two containers on your machine: a Ruby/Rails environment running the local server and a Postgres container where your database is stored.

## Set Up Instructions

To use this repository, you'll need to follow these steps:

* If you don't have Docker on your local machine, go to [Docker](https://docs.docker.com/get-docker/) and download the Docker Desktop for your personal environment (Windows, Mac, or Linux). Follow all the steps in the documentation to install Docker on your machine.

* If necessary, install [Docker Compose](https://docs.docker.com/compose/install/). You will probably not need to do this as Docker Desktop for Mac and Windows already includes Docker Compose.

* Once you've installed Docker, you're ready to clone this repository and `cd` into the repo.

* Run `docker-compose up` to run the local server at `localhost:3000`.

* You can update the Rails code in this repository as needed.

### Running Shell Commands

To access a shell environment to run `rails c`, run migrations, or run other `rake` and `rails` tasks such as `rails routes`, you'll need to do the following.

* First, you need to get the container ID for your web application. Open a new terminal window and run `docker ps`.

```
CONTAINER ID   IMAGE                             COMMAND                  CREATED          STATUS          PORTS                    NAMES
1c91fd563023   ruby-rails-docker-container_web   "entrypoint.sh bash …"   16 seconds ago   Up 14 seconds   0.0.0.0:3000->3000/tcp   ruby-rails-docker-container_web_1
4e59f148089f   postgres:12.1                     "docker-entrypoint.s…"   4 minutes ago    Up 15 seconds   5432/tcp                 ruby-rails-docker-container_db_1
```

Copy the container ID for `ruby-rails-docker-container_web` (in the example above, it's `1c91fd563023`).

* Next, you need to open a shell environment for the container with the following command: `docker exec -it [CONTAINER_ID] sh`. Replace `[CONTAINER_ID]` with the container ID you copied after running `docker ps`. Using the container ID above, the command would be `docker exec -it 1c91fd563023`.

* This will open a shell where you can run `rails c` and any `rake` or `rails` commands in the container's environment.

* While you can also connect to the container running Postgres, it's neither necessary nor recommended.

* If you need to re-run a process and you get the following error `Bind for 0.0.0.0:3000 failed: port is already allocated`, that means your processes are still running. Run `docker ps` to find the container IDs for running Docker processes and then run `docker stop [CONTAINER_ID]` where `[CONTAINER_ID]` is the container ID of the process. Use this whenever you need to manually stop a Docker process.

To read more about the process in Docker's documentation, see [Quickstart: Compose and Rails](https://docs.docker.com/compose/rails/).