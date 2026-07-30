# Mailpit service for Kubernetes on Wodby

Run Mailpit as a reusable Kubernetes application service with Wodby.

This repository defines the Wodby service manifests and operational
configuration for Mailpit.

- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Wodby stacks using this service

- [Django application stack](https://github.com/wodby/stack-django)
- [Drupal application stack](https://github.com/wodby/stack-drupal)
- [FastAPI application stack](https://github.com/wodby/stack-fastapi)
- [Flask application stack](https://github.com/wodby/stack-flask)
- [Go application stack](https://github.com/wodby/stack-go)
- [Laravel application stack](https://github.com/wodby/stack-laravel)
- [Mailpit application stack](https://github.com/wodby/stack-mailpit)
- [Next.js application stack](https://github.com/wodby/stack-nextjs)
- [Node.js application stack](https://github.com/wodby/stack-node)
- [PHP application stack](https://github.com/wodby/stack-php)
- [Python application stack](https://github.com/wodby/stack-python)
- [Rails application stack](https://github.com/wodby/stack-rails)
- [Ruby application stack](https://github.com/wodby/stack-ruby)
- [WordPress application stack](https://github.com/wodby/stack-wordpress)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `mailpit` |
| Type | Application service |
| Versions | `1.20` by default |
| Workloads | `main` (StatefulSet), primary |
| Containers | `mailpit` using `axllent/mailpit` |
| Endpoints | `mailpit`: TCP 1025, HTTP 8025 |
| Volumes | Data |
| Helm | chart `oci://registry-1.docker.io/wodby/mailpit`; version `0.2.1` |

## Use this service

Use this service through one of the Wodby application stacks listed above, or
reference `mailpit` from a custom Wodby stack.

A service is a reusable component and does not deploy by itself. The stack
defines its links, settings, versions, resources, and relationship to the rest
of the application.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Keep service, workload, container, endpoint, link, volume, config, and
derivative names stable unless dependent stacks and app-level overrides are
updated at the same time.

Validate the manifests with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
