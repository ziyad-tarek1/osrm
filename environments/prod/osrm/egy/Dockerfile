FROM ghcr.io/project-osrm/osrm-backend:latest-debug

# RUN apt update && apt install wget -y && wget http://download.geofabrik.de/africa/egypt-latest.osm.pbf

RUN apk update && apk add --no-cache wget && wget http://download.geofabrik.de/africa/egypt-latest.osm.pbf

RUN osrm-extract -p /opt/car.lua egypt-latest.osm.pbf || echo "osrm extract failed"

RUN osrm-partition egypt-latest.osrm && osrm-customize egypt-latest.osrm

CMD ["osrm-routed", "--algorithm", "mld", "egypt-latest.osrm"]
