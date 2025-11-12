> [!NOTE]
> This recipe app is one of our _single-service utility apps_ - standalone and reusable services, that can be easily imported to any project.

### 1. Import the Service

That's it - simply [import](https://docs.zerops.io/references/import#yaml-configuration-basics) the following YAML as a service to an existing project,
or append the service definition to your _project_ import YAML.

```yaml
services:
  # Deploy the 'mailpit' service and expose it
  # publicly on HTTPS via Zerops subdomain. 
  - hostname: mailpit
    type: alpine@3.21
    buildFromGit: https://github.com/zerops-recipe-apps/mailpit-app
    enableSubdomainAccess: true
```

This recipe app uses the following YAML:

```yaml
zerops:
  # Simple utility service. Download and run
  # the https://github.com/axllent/mailpit.
  - setup: mailpit
    build:
      base: alpine@latest
      buildCommands:
        - sh download-mailpit.sh
      # Deploy the downloaded binary.
      deployFiles: ./mailpit
    # Check that the Mailpit is running correctly,
    # after it was deployed.
    deploy:
      readinessCheck:
        httpGet:
          port: 8025
          path: /
    run:
      # No required runtime dependencies.
      base: alpine@latest
      ports:
        # Define port with 'httpSupport=true' for web UI.
        - port: 8025
          httpSupport: true
        # SMTP sink port.
        - port: 1025
      # Run the downloaded binary.
      start: ./mailpit
```
