# Access to agent's local ports (127.0.0.1)

If you need to access the local ports of the currently connected agent, there's a "magic" CIDR hardcoded in Ligolo-ng: *240.0.0.0/4* (This is an unused IPv4 subnet).
If you query an IP address on this subnet, Ligolo-ng will automatically redirect traffic to the agent's local IP address (127.0.0.1).

Example:

```
$ sudo ip route add 240.0.0.1/32 dev ligolo
$ nmap 240.0.0.1 -sV
Starting Nmap 7.93 ( https://nmap.org ) at 2023-12-30 22:17 CET
Nmap scan report for 240.0.0.1
Host is up (0.023s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 8.4p1 Debian 5+deb11u3 (protocol 2.0)
8000/tcp open http SimpleHTTPServer 0.6 (Python 3.9.2)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.16 seconds
```