# docker-mongo-migrator

A quick Docker image for running MongoDB Migrations

### Installation

```bash
docker build -t mongo-migrator .
```

### Running migrations


Make sure that the `mongo-migrator` docker image has been created. Then run the migrations. You can remove `1` to run all migrations.


```bash
docker run --network host migrator -path=/migrations/ -database "mongodb://localhost:27017/test" up 1
```

### Removing migrations

If you want to remove a migration

```bash
docker run --network host migrator -path=/migrations/ -database "mongodb://localhost:27017/test" down 1
```

### Running migrations without docker

```bash
docker run -v absolute/path/to/your/migrations/folder --network host migrate/migrate -path=/migrations/ -database "mongodb://localhost:27017/test" up 1
```

### Adding new migrations

* The **naming format** is `{migrationNumber}_{description}_{addOrRemoveMigration}.json`
* Make sure that you **increment** the `migrationNumber` **correctly**
* Each new migration has **2 files** (`up` and `down`).
* The `.up.json` file will be executed when **adding** migrations
* The `.down.json` file will be executed when **removing** migrations
* Each migration works with MongoDB [runCommands](https://docs.mongodb.com/manual/reference/command/)