---
order: 200
icon: workflow
---

# Multi Repo Configuration

Voyage supports multi-repository deployments. This is supported by referencing an additional repository as a service
inside the `.voyage` config file. The current repo executing the deployment is considered the primary repository.
The `api` repository in this case will use the Dockerfile in the root of the additional repo just like normal.
When using an external repo however the only `.voyage` configuration that will be read will be the primary repo
executing the deployment.

You may specify which branch to use from the external repo. If an `externalBranch` is not provided, Voyage will look
for a matching branch name as the current branch being deployed from the primary repo. If Voyage can not find a matching branch it will default
to the `externalBranchDefault` field. If that field is not provided it
will lastly fallback to `master`.

In order to reference the `api` service url inside the `app` service, Voyage automatically injects environment variables
into each container with a format of `VOYAGE_SERVICE_{SERVICE_NAME}_URL`. So in this case the referenced url would be
`VOYAGE_SERVICE_API_URL`.

In the case you would like your service variables named differently you may cast them to a different value in the config file.

To learn more about adding environment variables in Voyage and accessing service url's, see [Using Environment Variables](/docs/environment).

Here is a simple example.

```yaml
services:
  app:
    context: ./
    primary: true
    exposePort: 3000
  api:
    context: ./
    externalUrl: https://github.com/voyageapps/api-service
    externalBranch: feat/new-feat
    # Fallback if no matching branch name
    externalBranchDefault: staging
    exposePort: 3001
    environment:
      - name: API_URL
        value: ${VOYAGE_SERVICE_API_URL}
```
