---
order: 200
icon: project
---

# Projects

# Creating a project

When connecting a project/repo to Voyage, you may choose between "connected" projects
or "custom" projects.

Connected projects are meant to be connected to a repo and deploy PR's on demand and
also update the deployments when new commits are pushed. When a PR is closed or merged,
that deployment will automatically be torn down.

Custom projects are one off deployments from either an internal or external repository.
When creating a custom deployment, you can provide a Github url to a project that either matches
a voyage preset or contains a Voyage config file. Once I connect the repo, I can select the branch that
I would like to deploy with Voyage.

When deploying a custom deployment it must either adhear to a Voyage preset or contain a Voyage
configuration file, otherwise it will not deploy.

# Connecting Projects

You may manage access to various repositories within organizations you have access to by
selecting the dropdown in the top left and choosing "Update Voyage Access". This will allow
you to manage with repositories the Voyage application can access and deploy from.
