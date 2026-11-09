# book-lib

Book library REST service: Spring Boot 3, Spring Data JPA, PostgreSQL.
The first version of the project; see also book-soap and book-graphql
(same model, SOAP and GraphQL APIs).

## Run

PostgreSQL (example with Docker):

    docker run --name book-pg -e POSTGRES_PASSWORD=pass -p 5432:5432 -d postgres:16

Application:

    DB_PASSWORD=pass ./mvnw spring-boot:run

Settings (environment variables): `DB_URL`, `DB_USERNAME`, `DB_PASSWORD`
(required).

`schema-notes.sql` holds working notes on the PostgreSQL tables and enum
types (`book_library`, `book_status`, `book_credential`). It also contains
`DROP` statements, so do not run it as a whole.

## API

Base path `/api` (port 8080):

| Method | Path | Parameters |
|---|---|---|
| GET | `/books` | |
| GET | `/books-dto` | |
| GET | `/books-by-genre` | `bookGenre` |
| GET | `/books-by-genre-and-pages` | `bookGenre`, `min`, `max` |
| GET | `/books-by-genre-and-pages-ordered` | `bookGenre`, `min`, `max` |
| GET | `/books-free` | |
| GET | `/books-reserved` | |
| PUT | `/reserve-book` | `title` |
| PUT | `/free-book` | `title` |

Example: `http://localhost:8080/api/books-by-genre?bookGenre=Fantasy`

Genres: Fantasy, Horror, Drama, Comedy, NonFiction.

## Test

    ./mvnw test

Tests use an in-memory H2 database (profile `test`), no PostgreSQL needed.
