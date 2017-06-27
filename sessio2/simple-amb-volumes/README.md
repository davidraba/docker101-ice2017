# Aplicatiu connectat a BBDD amb volum de host mapejat

```
node:
    build: ./node-vol
    links:
        - redis
    ports:
        - "80:8080"
    volumes:
        - /src:/src
redis:
    image: redis
    ports:
        - "6379"
```
