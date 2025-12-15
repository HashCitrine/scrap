# FRP (Fast Reverse Proxy)
> frp is a fast reverse proxy that allows you to expose a local server located behind a NAT or firewall to the Internet.

# FRPS (server)
- 이미지 : https://hub.docker.com/r/snowdreamtech/frps
- docker compose
  ``` yaml
  version: "3.8"

  services:
    frpc:
      image: snowdreamtech/frpc:latest
      container_name: frpc
      restart: unless-stopped
      volumes:
        - ./frpc.toml:/etc/frp/frpc.toml
      environment:
        - TZ=Asia/Seoul
      networks:
        - frp_shared_nw
      depends_on:
        - api
      healthcheck:
        test: [ "CMD", "pidof", "frpc" ]
        interval: 30s
        timeout: 10s
        retries: 3
        start_period: 10s
  
  networks:
    frp_shared_nw:
      external: true
  ```
- frpc.toml
  ``` toml
  # frpc.toml
  serverAddr = "${FRP_SERVER_IP_OR_DOMAIN}"
  serverPort = ${FRP_SERVER_PORT}
  
  auth.token = "${FRP_SERVER_AUTH_TOKEN}"
  
  loginFailExit = false
  
  log.level = "trace"
  
  transport.tls.enable = false
  
  [[proxies]]
  name = "${FRP_SERVICE_NAME}"
  type = "http"
  localIP = "${FRP_SERVICE_CONTAINER_NAME}"
  localPort = ${FRP_SERVICE_CONTAINER_PORT}
  subdomain = "${FRP_SERVICE_SUB_DOMAIN}"
  ```
