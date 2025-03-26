# Configuration File

Since Ligolo-ng v0.8, the `proxy` supports a configuration file for advanced features.

```yaml
agent:
    deadbeefcafe:
        autobind: false
        interface: ligolo
interface:
    ligolosample:
        routes:
            - 10.254.0.0/24
            - 10.255.0.0/24
web:
    behindreverseproxy: false
    corsallowedorigin:
        - https://webui.ligolo.ng
    debug: false
    enabled: false
    enableui: true
    listen: 127.0.0.1:8080
    logfile: ui.log
    secret: 3383861a48e1332583e5d8cd9946d24b98be780e0c64581d693cb4ff50a68a68
    tls:
        alloweddomains: []
        autocert: false
        certfile: ""
        enabled: false
        keyfile: ""
        selfcert: false
        selfcertdomain: ligolo
    trustedproxies:
        - 127.0.0.1
    users:
        ligolo: $argon2id$v=19$m=32768,t=3,p=4$De5gVDnUWkQgsHe60gpCnA$S6UYLKSXlcCO8jr05zCW6BibdIYQFwdYxoAdRJPwAig
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

!!! warning

    WebUI is *disabled* by default, set `enabled: true` on the configuration file to enable it!

### Settings

```yaml
web:
    behindreverseproxy: false
    corsallowedorigin:
        - https://webui.ligolo.ng
    debug: false
    enabled: false
    enableui: true
    listen: 127.0.0.1:8080
    logfile: ui.log
    secret: 3383861a48e1332583e5d8cd9946d24b98be780e0c64581d693cb4ff50a68a68
    tls:
        alloweddomains: []
        autocert: false
        certfile: ""
        enabled: false
        keyfile: ""
        selfcert: false
        selfcertdomain: ligolo
    trustedproxies:
        - 127.0.0.1
    users:
        ligolo: $argon2id$v=19$m=32768,t=3,p=4$De5gVDnUWkQgsHe60gpCnA$S6UYLKSXlcCO8jr05zCW6BibdIYQFwdYxoAdRJPwAig
```

- behindreverseproxy: Set to `true` is running behind a reverse-proxy
- corsallowedorigin: Set the list of origins that should be allowed to make cross-origin calls
- debug: run the webserver with debug enabled, which is a lot noisier
- enabled: enable or disable the API (default: false)
- enableui: expose the ligolo-ng WebUI (default: true)
- listen: specify the listening IP and port
- logfile: specify where http logs should be stored
- secret: the JWT secret, automatically generated on first start
- tls: specify tls options, works like ligolo-ng proxy settings
- trustedproxies: trustedproxies set a list of network origins (IPv4 addresses, IPv4 CIDRs, IPv6 addresses or IPv6 CIDRs) from which to trust request's headers that contain alternative client IP.
- users: users allowed to connect to the web API

!!! tip

    You don't need to manually encrypt passwords using argon2id. If you specify a cleartext password, Ligolo-ng will automatically encrypt your password and update the configuration file.

