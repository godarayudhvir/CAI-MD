Here's a full example of a Docker Compose file for 
Wiki.js, using PostgreSQL, listening on port 80:

```yml
version: "3"
services:

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: wikijsdb
      POSTGRES_PASSWORD: ;j=ii6oJKEtqiQAjd4?1
      POSTGRES_USER: administrator
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: administrator
      DB_PASS: ;j=ii6oJKEtqiQAjd4?1
      DB_NAME: wikijsdb
    restart: unless-stopped
    ports:
      - "2002:3000"

volumes:
  db-data:
```

`DB_HOST` should match the service name (in this case, `db`).
 If `container_name` is specified for the service, its value should be used instead.

*For PostgreSQL*

- **DB_HOST** : Hostname or IP of the database
- **DB_PORT** : Port of the database
- **DB_USER** : Username to connect to the database
- **DB_PASS** : Password to connect to the database
- **DB_NAME** : Database name

*When connecting to a database server with SSL enforced:*

- **DB_SSL** : Set to either `1` or `true` to enable. *(optional, off if omitted)*
- **DB_SSL_CA** : Database CA certificate content, as a single line string (without spaces or new lines), without the prefix and suffix lines. *(optional, requires 2.3+)*

*Alternative way to provide the database password, via a local file secret:*

- **DB_PASS_FILE**: Path to the mapped file containing to the database password. *(optional, replaces DB_PASS)*

*For SQLite only:*

- **DB_FILEPATH** : Path to the SQLite file



after first run wait for sometime
