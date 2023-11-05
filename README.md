# hideme_wg_oracle_arm64

## wireguard vpn client with privoxy and microsocks in docker

## its a hideme vpn client ONLY

```
docker run -d \
  --name=hideme_wg_oracle_arm64 \
  --net=bridge \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  -e TZ="Europe/Berlin" \
  -e LOCAL_NET=<YOUR LOCAL IP ADDR eg. 192.168.1.0/24> \
  -e HIDEME_SERVER=sg \
  -e HIDEME_USER=<"USER_ID"> \
  -e HIDEME_PASS=<"USER_PASS"> \
  -p 8080:8080/tcp \
  -p 1080:1080/tcp \
  -v /config/hideme/:/config:rw \
  --cap-add=NET_ADMIN \
  --device /dev/net/tun \
  --sysctl net.ipv6.conf.all.disable_ipv6=1 \
  --privileged
  kartikbhalla/hideme_wg_oracle_arm64
```

## Environment Variables

LOCAL_NET - CIDR mask of the local IP addresses which will acess the proxy and bypass it, comma seperated \
HIDEME_SERVER - HideMe Server to use \
HIDEME_USER - your HideMe username for your vpn \
HIDEME_PASS - your HideMe password for your vpn \
HIDEME_SOCKS - set to `off` to disable \
HIDEME_PRIVOXY - set to `off` to disable \

privileged only needed in case of config directory is write protected

TZ - Timezone, not relevant for function

port 8080 privoxy \
port 1080 socks proxy

## hideme.client will replace dns servers and has a killswitch included, also reconnections are set to check every 3 minutes in case of disconnects

thanks to this nice app by hideme

https://github.com/eventure/hide.client.linux
