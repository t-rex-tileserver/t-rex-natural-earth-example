sw = t-rex
result_csv = results_seed.csv
ts = $(shell date '+%Y-%m-%dT%TZ')
region_bbox = 8.415527,45.174293,12.711182,47.428087

seed_world: $(result_csv)
	time -f "$(ts),$(sw),$@,%E,%U,%S" -a -o $(result_csv) t_rex generate --config mvtbench.toml --maxzoom=10 --tileset=ne --extent=-180,-90,180,90

seed_region: $(result_csv)
	time -f "$(ts),$(sw),$@,%E,%U,%S" -a -o $(result_csv) t_rex generate --config mvtbench.toml --maxzoom=10 --tileset=ne --extent=$(region_bbox)

seed_region_4: $(result_csv)
	time -f "$(ts),$(sw),$@,%E,%U,%S" -a -o $(result_csv) sh -c 't_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=0 --tileset=ne --extent=$(region_bbox) & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=1 --tileset=ne --extent=$(region_bbox) & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=2 --tileset=ne --extent=$(region_bbox) & \
	t_rex generate --config mvtbench.toml --maxzoom=10 --progress=false --nodes=4 --nodeno=3 --tileset=ne --extent=$(region_bbox)'

$(result_csv):
	echo time_started,software,test_name,real,user,sys >$@

http:
	# 1 connection
	docker run --rm --net=host -v $$PWD:/bench williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 4 --timeout 8 -t 1 -s /bench/httpbench.lua http://127.0.0.1:6767
	# 4 connections
	docker run --rm --net=host -v $$PWD:/bench williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 4 --timeout 8 -t 4 -s /bench/httpbench.lua http://127.0.0.1:6767
	# 32 connections
	docker run --rm --net=host -v $$PWD:/bench williamyeh/wrk -H 'Accept-Encoding: gzip' -H 'Connection: keep-alive' --latency -d 5 -c 32 --timeout 8 -t 4 -s /bench/httpbench.lua http://127.0.0.1:6767

stats:
	find /tmp/mvtcache/ne -name '*pbf' | wc -l
	du -s /tmp/mvtcache/ne

clean:
	rm -rf /tmp/mvtcache
