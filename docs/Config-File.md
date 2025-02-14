# Configuration File

Since Ligolo-ng v0.8, the `proxy` supports a configuration file for advanced features.

```yaml
agent:
    deadbeefcafe:
        autobind: false
        interface: ligolo
interface:
    ligolo:
        routes:
            - 10.55.0.0/24
    massivebyte:
        routes:
            - 10.56.0.0/24
web:
    corsallowedorigin:
        - '*'
    debug: false
    enabled: true
    listen: :8080
    secret: 1107608060e80ba4dfadd6a1fbc9fb3f4367fbf0b84f505bab0caf4e769db54e
    trustedproxies:
        - 127.0.0.1
    users:
        ligolo: $argon2id$v=19$m=32768,t=3,p=4$KQNyNWbYX2rsrl5rvTzR0g$VwRGBk4Gwzu3cmKBH4eqjv/zP4QieYB1IA7liu5HTO8
```

## Agent

### Autobinding

The autobind feature allows agents to be automatically assigned to an interface when they log on.

To enable this feature, you need to specify the session identifier (by default, the agent's MAC address), the interface to which it will be attached, and set autobind to true.

```yaml
agent:
    deadbeefcafe:
        autobind: true
        interface: ligolo
```

The following lines should appear the next time the agent connects:

```
INFO[0001] Agent joined. id=deadbeefcafe name=nchatelain@nworkstation remote="127.0.0.1:56072"
INFO[0001] Starting autobind session: deadbeefcafe on interface ligolo 
INFO[0001] Starting tunnel to nchatelain@nworkstation (deadbeefcafe)
```

## Interface

### Automatic interfaces & routes

Tired of having to configure interfaces and routes every time?
You can now configure interfaces and routes in advance in the configuration file. As soon as you start a tunneling session, Ligolo-ng will take care of everything.

```yaml
interface:
    ligolo:
        routes:
            - 10.55.0.0/24
```

!!! info

    Each time you add an interface/route using Ligolo-ng commands like interface_create, route_add, it will be automatically registered in the configuration file.

## Web

Ligolo-ng now has an experimental Web API, capable of controlling all cli interface functions via HTTP calls.

### Settings

```yaml
web:
    corsallowedorigin:
        - '*'
    debug: false
    enabled: true
    listen: :8080
    secret: 1107608060e80ba4dfadd6a1fbc9fb3f4367fbf0b84f505bab0caf4e769db54e
    trustedproxies:
        - 127.0.0.1
    users:
        ligolo: $argon2id$v=19$m=32768,t=3,p=4$KQNyNWbYX2rsrl5rvTzR0g$VwRGBk4Gwzu3cmKBH4eqjv/zP4QieYB1IA7liu5HTO8
```

- corsallowedorigin: Set the list of origins that should be allowed to make cross-origin calls
- debug: run the webserver with debug enabled, which is a lot noisier
- enabled: enable or disable the API (default: false)
- secret: the JWT secret, automatically generated on first start
- trustedproxies: trustedproxies set a list of network origins (IPv4 addresses, IPv4 CIDRs, IPv6 addresses or IPv6 CIDRs) from which to trust request's headers that contain alternative client IP.
- users: users allowed to connect to the web API

!!! tip

    You don't need to manually encrypt passwords using argon2id. If you specify a cleartext password, Ligolo-ng will automatically encrypt your password and update the configuration file.

