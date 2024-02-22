# workshop3
Run the following command to start your application.

```console
$ docker compose up --build
```
## Add records to the database

For the sample application, you must access the database directly to create sample records.

You can run commands inside the database container using the `docker exec`
command. Before running that command, you must get the ID of the database
container. Open a new terminal window and run the following command to list all
your running containers.

```console
$ docker container ls
```

You should see output like the following.

```console
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS                        PORTS                  NAMES
cb36e310aa7e   docker-dotnet-server   "dotnet myWebApp.dll"    About a minute ago   Up About a minute             0.0.0.0:8080->80/tcp   docker-dotnet-server-1
39fdcf0aff7b   postgres               "docker-entrypoint.s…"   About a minute ago   Up About a minute (healthy)   5432/tcp               docker-dotnet-db-1
```

In the previous example, the container ID is `39fdcf0aff7b`. Run the following command to start a bash shell in the postgres container. Replace the container ID with your own container ID.

```console
$ docker exec -it 39fdcf0aff7b bash
```

Then run the following command to connect to the database.

```console
postgres@39fdcf0aff7b:/$ psql -d example -U postgres
```

And finally, insert a record into the database.

```console
example=# INSERT INTO "Students" ("ID", "LastName", "FirstMidName", "EnrollmentDate") VALUES (DEFAULT, 'Whale', 'Moby', '2013-03-20');
```

You should see output like the following.

```console
INSERT 0 1
```

Close the database connection and exit the container shell by running `exit` twice.

```console
example=# exit
postgres@39fdcf0aff7b:/$ exit
```
