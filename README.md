t-rex NaturalEarth example
==========================

This repo contains t-rex examples using NaturalEarth data.

The main example uses the `natural-earth-quickstart` style from the Tegola web demo.


DB Setup
--------

    # Set Postgresql environment variables when needed: PGHOST, PGPORT, PGUSER, PGPASSWORD
    cd data
    make createdb

### From GeoPackage

    make gpkgrestore

### From raw data

Data: NaturalEarth 4.1 ([Site](http://www.naturalearthdata.com/) / [Github](https://github.com/nvkelso/natural-earth-vector)) is used as test data.

    make data import import_points optimize


Run quickstart example
----------------------

Set `TREX_DATASOURCE_URL` variable according to your DB setup.

DB connection via socket:

    export TREX_DATASOURCE_URL=postgresql://$USER@%2Frun%2Fpostgresql/naturalearth4

DB connection via TCP:

    export TREX_DATASOURCE_URL=postgresql://user:pass@localhost/naturalearth4

Start tile server:

    t_rex serve --config natural-earth.toml

Open map:

    http://127.0.0.1:6767/maps/map.html


Run country example
-------------------

Start tile server:

    t_rex serve --config natural-earth-countries.toml

Open map:

    http://127.0.0.1:6767/maps/map-countries.html
