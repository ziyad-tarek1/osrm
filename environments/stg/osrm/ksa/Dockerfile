FROM ghcr.io/project-osrm/osrm-backend:latest-debug

# Install wget in a separate layer for better caching
RUN apk update && apk add --no-cache wget

# Download OSM data in a separate layer (will be cached if unchanged)
RUN wget http://download.geofabrik.de/asia/gcc-states-latest.osm.pbf

# Process OSM data with OSRM tools in separate layers for better caching
RUN osrm-extract -p /opt/car.lua gcc-states-latest.osm.pbf || echo "osrm extract failed"

# Partition and customize in separate layer (most expensive operation)
RUN osrm-partition gcc-states-latest.osrm && osrm-customize gcc-states-latest.osrm

CMD ["osrm-routed", "--algorithm", "mld", "gcc-states-latest.osrm"]
