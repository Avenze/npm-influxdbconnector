# npm-influxdbconnector

Installation Guide

1) Create a bucket on InfluxDB, remember it's name for later.
2) Create a separate user for the bucket, or use the default account created at installation. (https://docs.influxdata.com/influxdb/v2.3/users/create-user)
3) Download GeoLite2-City.mmdb, (wget https://git.io/GeoLite2-City.mmdb)
4) Start the Docker container using the command provided below.
5) Add data source into grafana
6) Import the dashboard file and set the new data source

```
docker run --name npmgraf -d -it \
-v /home/docker/nginx-proxy-manager/data/logs:/logs \
-v /home/docker/nginx-proxy-manager/GeoLite2-City.mmdb:/GeoLite2-City.mmdb \
-e HOME_IPS="192.168.0.*\|192.168.10.*" \
-e INFLUX_USER=admin -e INFLUX_PW=password \
-e INFLUX_DB=bucket-name \
-e INFLUX_HOST=192.168.0.189 \
-e INFLUX_PORT=8086 \
makarai/nginx-proxy-manager-graf
```

Dashboard Worldmap Panel:

```
SELECT count("IP") AS "counts" FROM "ReverseProxyConnections" WHERE $timeFilter GROUP BY "latitude", "longitude", "IP"
```

![nginx](https://github.com/ma-karai/nginxproxymanagerGraf/blob/master/Screenshot%202021-02-14%20142221.png?raw=true)
