# Custom Vector Tiles from OpenStreetMap

A skeleton to start custom vector tile development from OpenStreetMap.
It contains an example mapping and source definition for buildings.

## Run Workflow

The entire project is structured components using Docker containers
to work together. Ensure you meet the prerequisites.

- Install [Docker](https://docs.docker.com/engine/installation/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

Start up the PostgreSQL database with the PostGIS extension.

```bash
docker-compose up -d postgres
```

Now download a OSM PBF extract and store it in the `./data` dir.

```bash
wget -P ./data https://s3.amazonaws.com/metro-extracts.mapzen.com/zurich_switzerland.osm.pbf
```

Import the OSM PBF.

```bash
docker-compose run import-osm
```

Import the required database schema (views, prepared tables and helper functions).

```bash
docker-compose run db-schema
```

Export the vector tiles for the planet.

```bash
docker-compose run export-vectortiles
```

To visualize and work with the vector tiles you can spin up Mapbox Studio
in a Docker container and visit `localhost:3000`.

Then open the vector tile source with `Browse` and choose from `/projects/vector-datasource.tm2source`.

```bash
docker-compose up mapbox-studio
```
