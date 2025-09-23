## fastapi-template

## Development

```
fba celery worker
fba celery beat
# admin:123456
fba celery flower
```

## virtualenv

```
uv sync
.\.venv\Scripts\activate
```

## Migrate

```
alembic revision --autogenerate
alembic upgrade head
```

## lint

```
pre-commit install
pre-commit run --all-files
```

## Acknowledgments

- [fastapi_best_architecture](https://github.com/fastapi-practices/fastapi_best_architecture)