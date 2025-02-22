# Creating a Ligolo-ng router

![Basic Tunnel](/assets/graphs/RouterTunnel.svg)

In this tutorial, we will showcase how you can create a Ligolo-ng router to allow various computers on your network to access the agent network (like a site-to-site VPN).

This tutorial will use *Pfsense*, but the steps are mostly the same on other Router OS:

- Install Ligolo-ng daemon
- Connect an agent
- Start the tunnel on a specific interface
- Create a route to the agent network
- Change firewall rules to allow access to the target network
