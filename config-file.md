---
order: 200
icon: file-code
---

# Config File

!!!
Pick and choose which options are for you depending on your project.
!!!

```yaml
services:
  app:
    # Base image to use to build app
    image: node
    # Providing commands to build app w/out a Dockerfile
    # Voyage will run these commands inside the base image above
    commands:
      - "npm i"
      - "node server.js"
    # Context is where we should start building/running the app (Helpful for building a sub-directory)
    context: ./
    # If no dockerfile is specified Voyage will look for a Dockerfile in specified context or root of project
    dockerfile: ./Dockerfile.voyage
    # One container should be primary defining which container should accept the incoming requests
    primary: true
    # If no exposePort is defined, Voyage will default to 80
    exposePort: 8000
    environment:
      - name: MOCK_DEPLOYMENT
        value: 1
      - name: DB_HOST
        value: 127.0.0.1
      - name: REDIS_URL
        value: redis://127.0.0.1:6379
      # Sensative secrets may be defined via the UI and consumed like below
      - name: SECRET_VALUE
        value: ${SECRET}
    database:
      image: postgres:11
      # When using images you may mount init files from your codebase
      mount:
        - ./init.sql:/docker-entrypoint-initdb.d/init.sql
      environment:
        - name: POSTGRES_USER
          value: "test"
    redis:
      image: redis
      environment:
        - name: ALLOW_EMPTY_PASSWORD
          value: "yes"
```
