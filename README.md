# zkcopy

Tool for fast copying ZooKeeper data between different clusters.
Originally it was developed for copying big volumes of configuration over WAN.

## Build

Requires [apache maven 3](https://maven.apache.org/).

```bash
mvn clean install
```

## Usage

```bash
java -jar target/zkcopy.jar --source server:port/path --target server:port/path
```

With [docker](https://hub.docker.com/r/ksprojects/zkcopy/), use following commands:

```bash
docker pull ksprojects/zkcopy
docker run --rm -it ksprojects/zkcopy --source server:port/path --target server:port/path --targetUsernamePassword=username:password
```

## Options

```
Usage: zkcopy [-hci] [--timeout=<sessionTimeout>] [-b=<batchSize>] [-m=<mtime>]
              -s=server:port/path -t=server:port/path [-tup=username:password]
              [-w=<workers>]
      --timeout=<sessionTimeout>
                              Session timeout in milliseconds
                                Default: 40000
  -b, --batchSize=<batchSize> Batch write operations into transactions of this
                                many operations. Batch sizes are limited by the
                                jute.maxbuffer server-side config, usually
                                around 1 MB.
                                Default: 1000
  -c, --copyOnly[=<copyOnly>] set this flag if you do not want to remove nodes
                                that are removed on source
  -h, --help                  display this help and exit
  -i, --ignoreEphemeralNodes[=<ignoreEphemeralNodes>]
                              set this flag to false if you do not want to copy
                                ephemeral ZNodes
  -m, --mtime=<mtime>         Ignore nodes older than mtime
                                Default: -1
  -s, --source=server:port/path
                              location of a source tree to copy
  -t, --target=server:port/path
                              target location
      -tup, --targetUsernamePassword=username:password
                              target username:password
  -w, --workers=<workers>     number of concurrent workers to copy data
                                Default: 10
```
