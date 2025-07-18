FROM ghcr.io/project-osrm/osrm-backend:latest-debug

# RUN apt update && apt install wget -y && wget http://download.geofabrik.de/asia/gcc-states-latest.osm.pbf

RUN apk update && apk add --no-cache wget && wget http://download.geofabrik.de/asia/gcc-states-latest.osm.pbf

RUN osrm-extract -p /opt/car.lua gcc-states-latest.osm.pbf || echo "osrm extract failed"

RUN osrm-partition gcc-states-latest.osrm && osrm-customize gcc-states-latest.osrm

CMD ["osrm-routed", "--algorithm", "mld", "gcc-states-latest.osrm"]
