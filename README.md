# Back-End-Development-Songs

Get Songs microservice built with Flask and MongoDB. It stores the lyrics of
the band's most popular songs and exposes a RESTful API over that resource,
using PyMongo to talk to the database.

## Environment Setup

- Repository created from the provided template.
- Environment initialized using `bin/setup.sh`.
- Python version: 3.9.x
- Virtual environment: backend-songs-venv
- Database: MongoDB, reachable through the `MONGODB_SERVICE`,
  `MONGODB_USERNAME` and `MONGODB_PASSWORD` environment variables.

## RESTful API Endpoints

| Action | Method | Return code | Body | URL Endpoint |
| ------ | ------ | ----------- | ---- | ------------ |
| Health | GET | 200 OK | `{"status": "OK"}` | `/health` |
| Count | GET | 200 OK | `{"count": 20}` | `/count` |
| List | GET | 200 OK | `{"songs": [{...}]}` | `/song` |
| Create | POST | 201 CREATED | `{"inserted id": {...}}` | `/song` |
| Read | GET | 200 OK | A song as json `{...}` | `/song/{id}` |
| Update | PUT | 201 CREATED | A song as json `{...}` | `/song/{id}` |
| Delete | DELETE | 204 NO CONTENT | `""` | `/song/{id}` |

A create request for an id that already exists returns 302 FOUND. A read,
update or delete request for an unknown id returns 404 NOT FOUND. An update
that changes nothing returns 200 OK with the message
`{"message": "song found, but nothing updated"}`.

## Running the service

```bash
MONGODB_SERVICE=localhost MONGODB_USERNAME=root MONGODB_PASSWORD=password \
  flask --app app run --debugger --reload
```

The server listens on http://127.0.0.1:5000

## Verifying the endpoints

Each endpoint was exercised with curl. The captured output for every graded
exercise is stored in the `evidence/` directory.
