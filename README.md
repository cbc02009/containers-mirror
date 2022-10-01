# Container Images Mirror

Images are hosted on Github Container Registry [here](https://github.com/orgs/k8s-at-home/packages?ecosystem=container&visibility=public).

## Purpose

This is to get around Docker Hub rate-limiting (100 pulls / 6 hours, or authenticated 200 pulls / 6 hours). It is considered a stop-gap until the maintainers of the applications below support a different Container Registry.

## Supported images

When upstream maintainers add support for an additional registry, the images here will be purged after awhile.

| Name                                                                                            | Upstream Issue                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [reloader](https://github.com/stakater/Reloader)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/stakater/Reloader/255)](https://github.com/stakater/Reloader/issues/255)                                               |

## Contributing

You can discover containers running in your cluster from Docker Hub by using the following command:

```
kubectl get pods --all-namespaces -o=jsonpath="{range .items[*]}{'\n'}{range .spec.containers[*]}{.image}{'\n'}{end}{end}" | sort | uniq | grep -Ev 'quay|gcr|ghcr|ecr' |  sed -e 's/docker\.io\///g' | sort | uniq
```

After you have determined some image you want to mirror, do the following:

- If not already created, create an issue upstream asking for them to support an additional registry.
- Open a PR adding a new application to the `apps` folder, update the `README.md` with the issue link, and then update `.github/renovate.json5` to auto merge it.
- Remind us to make the image public after the PR is merged ;)

this is just to run the action again.
