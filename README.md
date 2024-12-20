# pg-essentials

Utilities for managing PostgreSQL databases, including multi-tenant scenarios.

# Table of Contents

-   psql-example-connect
-   pg-build-linux
-   pg-build-macos
-   pg-install
-   pg-register-service
-   pg-addgroup
-   pg-adduser
-   psql-store-credential
-   pg-passwd
-   psql-backup

## psql-example-connect

Copy, paste, & season to taste! \
(basically just an alias for connecting to a specific db)

## pg-build

Statically\* compiles postgres for linux or macos.

```text
pg-build v1.0.0 - builds a portable, relocatable postgres from source

USAGE
    postgres-build <vendor-name> <pg-version>

EXAMPLE
    postgres-build 'custom' 17.0
```

\* it's not really _static_, but rather _bundled_ or _vendored_ - the dependencies are included in the `./lib/` folder.

## pg-install

```text
pg-install v1.0.0 - installs postgres via apt-get or apk

USAGE
    pg-install <version>

EXAMPLE
    pg-install 16
```

## pg-register-service

```text
pg-register-service v1.0.0 - register a postgres daemon for the current user

USAGE
    pg-register-service <port> [operating-system-user]

EXAMPLE
    pg-register-service 5432 app
```

## pg-addgroup

```text
pg-addgroup v1.0.0 - add a group role to hba for remote users with samename dbs

USAGE
    pg-addgroup [hostssl|host|etc] [group-name] [pg-port]

EXAMPLE
    pg-addgroup hostssl remote_users 5432

NOTE
    use 'host' rather than 'hostssl' if you terminate postgres' tls via proxy
```

## pg-adduser

```text
pg-adduser v1.0.0 - adds a remote user (and db of the same name) to a group role

USAGE
    pg-adduser <username-prefix> [port] [group-name]

EXAMPLE
    pg-adduser 'foobar' 5432 'remote_users'

NOTES
    - usernames consist of a prefix + random hex string
    - each username has exactly 1 database of exactly the same name
    - passwords are random base58 (url-safe) strings
```

## psql-store-credential

```text
psql-store-credential v1.0.0 - stores a credential in ~/.pgpass

USAGE
    [space] pg-addpass [pg-url]

EXAMPLES
    Prompt for PG_URL string
        pg-addpass
    Prefix with space and give PG_URL string
          pg-addpass 'postgress://user:pass@host:port/db?sslmode=verify-full'
    Parse PG_URL from .env file
        cat .env | grep PG_URL | cut -d'=' -f2- | pg-addpass

NOTES
    - query parameters will be *ignored* (ex: ?sslmode=)
    - passwords with ':' or '@' will not be parsed correctly
      (you may be able to enter them into ~/.pgpass manually)

WARNING
    remember to clear this command from your shell history if
    you don't want the password to be saved there
    (some shells omit commands if you prefix them with a space)
```

## pg-passwd

```text
pg-passwd v1.0.0 - reset a user's password

USAGE
    pg-passwd <user> [port]

EXAMPLE
    pg-passwd foobar-xxxxxx 5432
```

## psql-backup

```text
psql-backup v1.0.0 - creates portable (across instances) SQL schema & data backups

USAGE
    psql-backup <user> [host] [port] [dbname]

EXAMPLE
    psql-backup 'foobar-xxxxxx' 'pg-1.example.com' 5432 'foobar-xxxxxx'

NOTES
    - the username and database name should typically be the same
```

# Copying

Copyright (c) 2024 AJ ONeal <aj@bnna.net> \
Licensed under the MPL-2.0
