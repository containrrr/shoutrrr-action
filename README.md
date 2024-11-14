# Notifications using Shoutrrr in GitHub Actions

With this action, you can send notifications using
[Shoutrrr](https://containrrr.dev/shoutrrr) from your GitHub Actions
workflows.

Let's give an example:

```yaml
name: Deploy
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Some other steps needed for deploying
        run: ...
      - name: Shoutrrr
        uses: containrrr/shoutrrr-action@v1
        with:
          url: ${{ secrets.SHOUTRRR_URL }}
          title: Deployed ${{ github.sha }}
          message: See changes at ${{ github.event.compare }}.
```

The `url` is the Shoutrrr service URL as described in the [service
overview](https://containrrr.dev/shoutrrr/services/overview/). Service
URLs usually contains tokens or other information you should keep
confidential, so make sure you store the URL or at least the secret
parts of the URL in a GitHub secret.

Not all services support the `title` option. It's optional and you can
leave it out.

> [!NOTICE]
> This action is only supported on Linux runners.
> See https://docs.github.com/en/actions/sharing-automations/creating-actions/about-custom-actions#types-of-actions