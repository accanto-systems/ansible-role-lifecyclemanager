# Ansible Role - Stratoss&trade; Lifecycle Manager

Ansible Role for installing Stratoss&trade; Lifecycle Manager (Stratoss LM) in Kubernetes using Helm.

## Configure Stratoss LM packages

Installation of Stratoss LM requires a lm-helm-charts package, configure the location with either a http/https address or file path (on local machine):

```
# Http/Https path
lm_charts_package: http://myrepo:8080/lm-helm-charts/lm-helm-charts-2.0.0.tgz

# File path
lm_charts_package: /home/user/lm-helm-charts-2.0.0.tgz
```

If not using a docker registry then installation will also require a lm-docker-source package, configure the location with either a http/https address or file path (on local machine):

```
# Http/Https path
lm_docker_package: http://myrepo:8080/lm-docker-source/lm-docker-source-2.0.0.tgz

# File path
lm_docker_package: /home/user/lm-docker-source-2.0.0.tgz
```

Packages are only copied to the target machine if they do not already exist. To force an update of the existing packages, use:

```
lm_force_refresh_packages: True
```

## Using a Docker Registry

If preferred, you may pull Stratoss LM docker images from a registry:

```
lm_docker_strategy: from_registry
lm_docker_registry_host: registry_host
lm_docker_registry_port: 5001
```

## Uninstall Existing

Installation will only take place in 2 situations:

* there is no existing Stratoss LM installed (identified by searching for a helm release named `lm`)
* the existing lm release does not match the version to be installed by given packages (installations of lm-configurator and helm-foundation are ignored)

In the second case, a re-install can be forced using:

```
lm_force_reinstall: True
```