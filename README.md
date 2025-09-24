## fastapi-template

## UI

![img.png](imgs/analytics.png)
![img.png](imgs/workspace.png)
![img.png](imgs/user.png)
![img.png](imgs/redis.png)

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
- [vue-vben-admin](https://github.com/vbenjs/vue-vben-admin)