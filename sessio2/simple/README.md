# Aplicatiu connectat a BBDD

```
node:
    build: ./node
    links:
        - redis
    ports:
        - "80:8080"
redis:
    image: redis
    ports:
        - "6379"

```
