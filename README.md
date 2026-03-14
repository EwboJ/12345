# citext

`citext` is a PostgreSQL extension that provides a case-insensitive character string type: `citext`. Essentially, it internally calls `lower` when comparing values, so that `'FOO'::citext = 'foo'::citext` is true.

## Overview

The `citext` module provides a case-insensitive character string type, `citext`. Essentially, it internally calls `lower` when comparing values. Otherwise, it behaves almost exactly like `text`.

## Usage

```sql
CREATE EXTENSION citext;

CREATE TABLE users (
    nick CITEXT PRIMARY KEY,
    pass TEXT NOT NULL
);

INSERT INTO users VALUES ( 'larry',  md5(random()::text) );
INSERT INTO users VALUES ( 'Tom',    md5(random()::text) );
INSERT INTO users VALUES ( 'Damian', md5(random()::text) );
INSERT INTO users VALUES ( 'ROGER',  md5(random()::text) );
INSERT INTO users VALUES ( 'Modern', md5(random()::text) );

SELECT * FROM users WHERE nick = 'Larry';
```

The `SELECT` will return one tuple, even though the `nick` column value is `larry` and the query value is `Larry`.

## Features

- Case-insensitive comparison (`=`, `<>`, `<`, `<=`, `>`, `>=`)
- Case-insensitive pattern matching (`LIKE`, `ILIKE`, `~`, `~*`, etc.)
- Support for B-tree and hash indexes
- `min()` and `max()` aggregates
- Compatible with standard `text` functions

## Installation

Build and install as a standard PostgreSQL contrib module:

```sh
make
make install
```

Then load the extension in a database:

```sql
CREATE EXTENSION citext;
```

## Version History

The extension supports upgrade paths from version 1.0 through 1.8.