# No-Code OPCUA-to-MQTT Bridge

Bridge OPC-UA Data from a dedicated server to an MQTT Broker using Telegraf
and Docker Compose

## System Specs

### Docker Engine / Compose
Engine
```bash
Client:
 Version:           20.10.7
 API version:       1.41
 Go version:        go1.13.8
 Git commit:        20.10.7-0ubuntu5~20.04.2
 Built:             Mon Nov  1 00:34:17 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Desktop
 Engine:
  Version:          20.10.13
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.15
  Git commit:       906f57f
  Built:            Thu Mar 10 14:06:05 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.5.10
  GitCommit:        2a1d4dbdb2a1030dc5b01e96fb110a9d9f150ecc
 runc:
  Version:          1.0.3
  GitCommit:        v1.0.3-0-gf46b6ba
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```
Compose

```bash
Docker Compose version v2.3.3
```

### Containers

| Image Name | Version           |
|:----------:|:-----------------:|
| `telegraf` | `1.22-alpine`     |
| `eclipse-mosquitto` | `2.0.14` |


### OPC-UA Simulation Server

Use the [ProSys OPC Simulation Server][1] to simulate basic information

### MQTT Desktop Client

Use the [EMXQ MQTT Desktop Client][2]

## Usage

- Run the ProSys OPC Simulation Server and obtain the Connection Address from __Status__ tab
- Use the address in the compose file to set the `OPCUA_ENDPOINT_URL` env var
- In the Simulation Server, go to __Objects__ and start the simulation. The available Objects will
 be displayed under `Simulation::FolderType`
- Depending on your Setup, adapt the `namespace`, `identifier` and `identifier_type` in `telegraf.toml`

Bring the stack up using:

```bash
docker compose up
```

## Endpoints

- MQTT broker is available at `mqtt://localhost:1883`

Use the Desktop Client to connect to the broker and subscribe to the `telegraf/opcua/mqtt` topic
to subscribe to your OPC-UA data in ILP (Influx Line Protocol) format



[1]: https://downloads.prosysopc.com/opc-ua-simulation-server-downloads.php
[2]: https://www.emqx.com/en/products/mqttx