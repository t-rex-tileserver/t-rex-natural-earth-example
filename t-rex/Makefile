seed_world:
	time -p t_rex generate --config mvtbench.toml --maxzoom=10 --tileset=ne --extent=-180,-90,180,90

seed_region:
	time -p t_rex generate --config mvtbench.toml --maxzoom=10 --tileset=ne --extent=5.361328,45.336702,30.058594,58.950008

seed_region_4:
	time -p sh -c 't_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=0 --tileset=ne --extent=5.361328,45.336702,30.058594,58.950008 & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=1 --tileset=ne --extent=5.361328,45.336702,30.058594,58.950008 & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=2 --tileset=ne --extent=5.361328,45.336702,30.058594,58.950008 & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=3 --tileset=ne --extent=5.361328,45.336702,30.058594,58.950008'

http:
	# 1 connection
	docker run --rm --net=host williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 4 --timeout 8 -t 1 http://127.0.0.1:6767/ne/7/69/47.pbf
	# 4 connections
	docker run --rm --net=host williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 4 --timeout 8 -t 4 http://127.0.0.1:6767/ne/7/69/47.pbf
	# 32 connections
	docker run --rm --net=host williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 32 --timeout 8 -t 4 http://127.0.0.1:6767/ne/7/69/47.pbf

stats:
	find /tmp/mvtcache/ne -name '*pbf' | wc -l
	du -s /tmp/mvtcache/ne

clean:
	rm -rf /tmp/mvtcache
