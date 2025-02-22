# Advanced Tunnel / Double Pivot

!!! warning "Read the docs!"
    
    Make sure you have read the "Basic Tunneling" or "Quickstart" part of the documentation before following this guide!

Sometimes it is necessary to install a tunnel with a pivot. This is the case when you want to bounce onto a restricted network from a machine that doesn't have direct access to the Internet or to the Ligolo-ng daemon, but that machine can contact a host you've already compromised.

Thanks to Ligolo-ng's listeners feature, you can listen to a port on a Ligolo-ng agent, then retransmit connections to the Ligolo-ng proxy.

This tutorial simply explains how to establish a Ligolo-ng connection through a pivot.

![Advanced Tunnel Graph](/assets/graphs/AdvancedTunnel.svg)

## Tutorial

## On the Ligolo-ng Server

Start the `Ligolo-ng` server.

![Start Ligolo](/assets/tutorials/pivoting/start_ligolo.png)

## On Agent 1

Connect the `Agent 1` to the `Ligolo-ng` server.

![Connect Agent 1](/assets/tutorials/pivoting/agent_1_connect.png)

Create a Listener using the `listener_add` command.

`listener_add` takes two mandatory parameters:

- `--addr`: specifies which `ip:port` should be listening on the agent.
- `--to`: specifies where the connection will be relayed.


!!! info

    You can also use `--tcp` or `--udp` to specify which protocol to use. (Default is TCP)

If you run: `listener_add --addr 0.0.0.0:4444 --to 127.0.0.1:11601`:

- The agent will listen on `0.0.0.0:4444`
- Any connections on this `ip:port` will be relayed to the `11601` TCP local port of the Ligolo-ng daemon.

![Add Listener](/assets/tutorials/pivoting/agent_1_listener.png)

!!! info

    11601 is the default Ligolo-ng daemon server port. Any connections to the agent IP on port 4444 will be relayed to the Ligolo-ng local port!

You can confirm that the listener is running on `agent 1` by using the `listener_list` command:

![Listener list](/assets/tutorials/pivoting/agent_1_listener_list.png)


## On Agent 2

After running the `listener_add` command on the first agent, you can execute the Ligolo-ng agent on the second server (which does not have Internet access). 

Instead of specifying the `IP:PORT` of the Ligolo-ng daemon, you have to specify the IP of the first agent and the listening port used in `listener_add` (in our example, `4444`).

`$ ./ligolo-agent --connect 10.24.0.30:4444`

![Connect Agent 2](/assets/tutorials/pivoting/agent_2_connect.png)

After that, you should have a new agent connected to Ligolo-ng:

![Agent 2 connected](/assets/tutorials/pivoting/agent_2_join.png)

You can now setup the `Ligolo-ng` tunnel targeting the Agent 2 private network.

![Agent 2 Setup](/assets/tutorials/pivoting/agent_2_tunnel.png)

Once the tunnel is started, you can now access the private network resources!

![Access to Agent 2 Resources](/assets/tutorials/pivoting/agent_2_nmap.png)