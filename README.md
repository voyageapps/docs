---
icon: rocket
label: Quick Start
---

# Quick Start

1. [Sign up](https://app.voyageapp.io/sign-up) for a free account.

2. Connect a repository to Voyage.

3. Create your config file.

```yaml
# .voyage/config.yml
services:
  app:
    image: node
    context: ./
    primary: true
```

Once you have created a Voyage account, all you need to do is add a `.voyage` directory to your repository and create a `config.yml` similar to this snippet.
