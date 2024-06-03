# PT_Demo_GrateDatabaseMigration

PT_Demo_GrateDatabaseMigration is a simple demo to explain [Grate](https://github.com/erikbra/grate/tree/main).

![grate-execution-order](/res/grate-execution-order.jpg)

## Contents
- [Demo using Docker - Grate Docs Example](#demo-using-docker---grate-docs-example)
- [Demo using Docker - DK Example](#demo-using-docker---dk-example)
- [Links](#links)

## Demo using Docker - Grate Docs Example

1. Create the following folder structure:

- /src
    - /docker
        - /db
            - /dropDatabase // -1. Anytime
            - /createDatabase // 0. Anytime
            - /beforeMigration // 1. Everytime
            - /alterDatabase // 2. Anytime
            - /runAfterCreateDatabase // 3. Anytime
            - /runBeforeUp // 4. Anytime
            - /up // 5. One-Time
            - /runFirstAfterUp // 6. One-Time
            - /functions // 7. Anytime
            - /views // 8. Anytime
            - /sprocs // 9. Anytime
            - /triggers // 10. Anytime
            - /indexes // 11. Anytime
            - /runAfterOtherAnyTimeScripts // 12. Anytime
            - /permissions // 13. Everytime
            - /afterMigration // 14.  Everytime
        - /output

2. In `/up` folder, create SQL script `0001.CreateTable.Employee.sql`:

- /src
    - /docker
        - /db
            - /up
                - 0001.CreateTable.Employee.sql

```
CREATE TABLE employee (
  id int PRIMARY KEY, 
  name text,
  age int
);
```

3. In `/docker` folder, create file `docker-compose.yml`:

- /src
    - /docker
        - ddocker-compose.yml

```
version: "3.7"
services:
  db-migration:
    #build: .
    image: erikbra/grate:latest
    environment:
      # don't configure passwords here for real.  This is just a sample!
      APP_CONNSTRING: "Server=your-remote-public-ip-address:your-remote-port;Database=your-db;User Id=your-user-id;Password=your-user-pass;TrustServerCertificate=True"
      VERSION: "1.0.0.0"
      DATABASE_TYPE: "postgresql" # sqlite, oracle, postgresql, sqlserver, mariadb
    volumes:
      - ./db:/db
      - ./output:/output
```

## Demo using Docker - DK Example

## Links

Grate Docs - Directory Order:  
https://erikbra.github.io/grate/getting-started/#directory-run-order

Grate Docs - Configuration Options:
https://erikbra.github.io/grate/configuration-options/

Grate Repo - Example using Docker:  
https://github.com/erikbra/grate/tree/main/examples/docker
