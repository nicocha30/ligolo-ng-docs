---
authors:
    - Aurélien Chalot (@Defte_)
---

!!! note "Thanks to @Defte_"

    This documentation was written by @Defte_, many thanks to him!
    Using a reverse proxy will surely help you reduce your footprint, and avoid being detected!

If you ever need to hide the listener behind a reverse proxy (in our case Nginx), here is the Nginx configuration you will have to add:

```
server {
	server_name DNS_NAME;
	index index.html;
	location / {
		proxy_set_header Host $host;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Upgrade websocket;
		proxy_set_header Connection Upgrade;
		proxy_http_version 1.1; 
		proxy_pass https://LOCAL_IP:PORT;
	}
	listen 443 ssl;
	ssl_certificate /etc/letsencrypt/live/DNS_NAME/fullchain.pem;
	ssl_certificate_key /etc/letsencrypt/live/DNS_NAME/privkey.pem;
	include /etc/letsencrypt/options-ssl-nginx.conf; 
	ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}	
```

That use cas relies on let's encrypt to retrieve certificates so you will have to change the certificate and key suiting your needs. Once done, you can launch the ligolo proxy that way:

```
proxy -laddr https://LOCAL_IP:PORT -certfile /etc/letsencrypt/live/DNS_NAME/fullchain.pem -keyfile /etc/letsencrypt/live/DNS_NAME/privkey.pem
```

And the agent:

```
agent -connect https://DNS_NAME
```