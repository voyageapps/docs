---
order: 200
icon: gear
---

# Using Environment Variables

In order to add sensative values as environment variables to Voyage deployments, you will first configure these values in the Voyage UI.

![Env UI](https://cdn.voyageapp.io/docs/env_vars.jpg)

You would navigate to `https://app.voyageapp.io/projects/{PROJECT_ID}/settings/variables` and use the simple UI to add the needed variables.

You may add as many as you like. Then you may reference them in your Voyage config file like this example.

```yaml
services:
  app:
    context: ./Dockerfile
    environment:
      - name: SECRET_VALUE
        value: "${SECRET_VALUE}"
```

It's easy to reference a service's deployed url by using an example like this one.

```yaml
services:
  app:
    context: ./
    exposePort: 3001
    environment:
      - name: APP_URL
        value: "https://${VOYAGE_SERVICE_APP_URL}"
```

Another common use case would be passing a url for a second api service to a front-end service. Here is another example for how to accomplish this.

```yaml
services:
  frontend:
    context: ./
    primary: true
    exposePort: 3000
    environment:
      - name: API_URL
        value: "https://${VOYAGE_SERVICE_BACKEND_URL}/api/v1"
  backend:
    context: ./
    externalUrl: https://github.com/voyageapps/api-service
    exposePort: 3001
```

This allows every service to be able to discover the url of another one dynamically in the Voyage config. The format is `VOYAGE_SERVICE_{SERVICE_NAME}_URL`. The service name would be the key property for each service nested under `services` in the Voyage config file.

When running inside Voyage a build argument and environment variable `RUNNING_IN_VOYAGE=1` is automatically injected
into each build and deployment. This allows the developer to modify any build or startup scripts to build anything specific
for the Voyage environment.
