---
order: 200
icon: rows
---

# Docker Images

If your project is not configured for Docker don't sweat it. Voyage provides a handful of pre-built images to speed up your Voyage deployment process.

See the available images [here](https://github.com/voyageapps/public-images).
All images are hosted public on [Dockerhub](https://hub.docker.com/orgs/voyageapp/repositories).

## Databases

Voyage provides database convenient images which automatically set the initial database, user, and password to `voyage`.

```yaml
services:
  database:
    image: voyageapp/voyageapp/postgres:14.2
```
