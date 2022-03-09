# Firewalld Container Image

Firewall daemon (firewalld) container image with nftables as backend

## Run a firewalld instance

The firewalld container needs access to the host network and needs to run as
privileged container.

To start the container:

```
# podman run -d --rm --network host --privileged --name firewalld registry.opensuse.org/home/kukuk/container/firewalld:latest
```

## Persistent configuration files

By default changes to the default firewalld configuration are lost with a restart of the container, but the config files can be saved in a volume in `/etc/firewalld`:

```
# podman run -d --rm -v /etc/firewalld:/etc/firewalld -v /run/dbus/system_bus_socket:/run/dbus/system_bus_socket --network host --privileged --name firewalld registry.opensuse.org/home/kukuk/container/firewalld:latest
```

## Manage firewalld instance

The firewalld instance should be managed with the CLI via `podman exec`
after the container has been started:

```
# podman exec firewalld firewall-cmd ...
```

## firewalld documentation

The manual page for firewalld can be read with:

```
# podman run -it --rm registry.opensuse.org/home/kukuk/container/firewalld:latest man firewalld
```
