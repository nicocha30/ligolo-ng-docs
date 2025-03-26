# Ligolo-ng WebUI

Ligolo-ng WebUI is a new way of managing Ligolo-ng starting at Ligolo-ng version 0.8.

It is actively maintained by [L'Ami du Raisin](https://github.com/jeremiebedjai) and [Nicocha30](https://github.com/nicocha30).

!!! warning

    Update your settings in [ligolo-ng.yaml](/Config-File)!

## Enabling the Web API / UI

To enable the Web API and UI, you have to modify the `ligolo-ng.yaml` configuration file, and set the `web > enabled` parameter to true.

## Accessing the WebUI

You have three ways to use the WebUI:

- use the WebUI locally (recommended)
- build and deploy the WebUI: [ligolo-ng-web](https://github.com/nicocha30/ligolo-ng-web)
- use the [webui.ligolo.ng](https://webui.ligolo.ng/) website

### Using the WebUI locally

Once you modified the `enabled` and `enableui` in the `web` section of the `ligolo-ng.yaml` configuration file, you can start the ligolo-ng proxy.

By default, the WebUI is listening on `127.0.0.1:8080`. At startup, Ligolo-ng will tell you where the API is located:

`INFO[0000] Starting Ligolo-ng Web, API URL is set to: http://127.0.0.1:8080`

You should now be able to access the webUI.

![webui login](/assets/tutorials/web/login.png)

!!! info

    By default, the credentials are `ligolo:password`. *You should change the passwords in `ligolo-ng.yaml`.*

## Features

### Agent

On the **Agent** page, you can see all connected agents. You can also setup the tunneling, or use autoroute.

![agents](/assets/tutorials/web/agents.png)

![autoroute](/assets/tutorials/web/autoroute.png)

### Interfaces

On the **Interfaces** page, you can setup interfaces and routes.

![interfaces](/assets/tutorials/web/interfaces.png)

![new route](/assets/tutorials/web/newroute.png)


### Listeners

On the **Listeners** page, you can setup listeners.

![listeners](/assets/tutorials/web/listeners.png)

## Troubleshooting

### Failed to fetch when login in

This error can be caused by:

- a bad "API URL";
- the API URL is not in allowed origins (`corsallowedorigin` in `ligolo-ng.yaml`). 