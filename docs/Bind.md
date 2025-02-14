# Agent as server (Bind Connection)

The Ligolo-ng agent can operate using a bind connection (i.e. acting as a server).

Instead of using the `--connect [ip:port]` argument, you can use `--bind [ip:port]` so the agent start listening to connections.

After that, the proxy can connect to the agent using the `connect_agent` command.

In a terminal:
```
» ligolo-agent -bind 127.0.0.1:4444                                                                                                                                                                   
WARN[0000] TLS Certificate fingerprint is: 05518ABE4F0D3B137A2365E0DE52A01FE052EE4C5A2FD12D8E2DD93AED1DD04B 
INFO[0000] Listening on 127.0.0.1:4444...               
INFO[0005] Got connection from: 127.0.0.1:53908         
INFO[0005] Connection established                        addr="127.0.0.1:53908"
```

In ligolo-ng proxy:

```
ligolo-ng » connect_agent --ip 127.0.0.1:4444
? TLS Certificate Fingerprint is: 05518ABE4F0D3B137A2365E0DE52A01FE052EE4C5A2FD12D8E2DD93AED1DD04B, connect? Yes
INFO[0021] Agent connected.                              name=nchatelain@nworkstation remote="127.0.0.1:4444"
```
