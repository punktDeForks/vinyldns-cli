[![Docker Automated build](https://img.shields.io/docker/automated/vinyldns/vinyldns-cli.svg?style=flat)](https://hub.docker.com/r/vinyldns/vinyldns-cli/)
[![Build Status](https://travis-ci.org/vinyldns/vinyldns-cli.svg?branch=master)](https://travis-ci.org/vinyldns/vinyldns-cli)

# vinyldns-cli

A Golang-based CLI for the [vinyldns](https://github.com/vinyldns/vinyldns) DNS as a service API.

## Installation

Download the desired pre-compiled executable [release](https://github.com/vinyldns/vinyldns-cli/releases) version
for your operating system.

For example, to install version 0.7.0 on Mac OS:

```
wget https://github.com/vinyldns/vinyldns-cli/releases/download/v0.7.0/vinyldns_0.7.0_darwin_x86_64

chmod +x vinyldns_0.7.0_darwin_x86_64

./vinyldns_0.7.0_darwin_x86_64 --help
```

### Compiling from Golang source

Alternatively, if you choose to compile from Golang source code:

* install Golang
* set up your `$GOPATH`
* `go get github.com/vinyldns/vinyldns-cli`
* `cd $GOPATH/github.com/vinyldns/vinyldns-cli && make`

## Usage

```
vinyldns --help
```

Supported commands:

```
COMMANDS:
     groups              groups
     group               group --group-id <groupID>
     group-delete        group-delete --group-id <groupID>
     group-admins        group-admins --group-id <groupID>
     group-members       group-members --group-id <groupID>
     group-activity      group-activity --group-id <groupID>
     zones               zones
     zone                zone --zone-id <zoneID>
     zone-delete         zone-delete --zone-id <zoneID>
     zone-connection     zone-connection --zone-id <zoneID>
     zone-changes        zone-changes --zone-changes <zoneID>
     record-set-changes  record-set-changes --zone-id <zoneID>
     record-set          record-set --zone-id <zoneID> --record-set-id <recordSetID>
     record-set-change   record-set-change --zone-id <zoneID> --record-set-id <recordSetID> --change-id <changeID>
     record-set-create   record-set-create --zone-id <zoneID> --record-set-name <recordSetName> --record-set-type <type> --record-set-ttl <TTL> --record-set-data <rdata>
     record-set-delete   record-set-delete --zone-id <zoneID> --record-set-id <recordSetID>
     record-sets         record-sets --zone-id <zoneID>
     batch-changes       batch-changes
     help, h             Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --host value                    vinyldns API Hostname [$VINYLDNS_HOST]
   --access-key value, --ak value  vinyldns access key [$VINYLDNS_ACCESS_KEY]
   --secret-key value, --sk value  vinyldns secret key [$VINYLDNS_SECRET_KEY]
   --help, -h                      show help
   --version, -v                   print the version
```

Example usage:

```
vinyldns \
  --host https://my-vinyldns.com \
  --access-key 123 \
  --secret-key 456 \
  zones

+--------------------+--------------------------------------+
|        NAME        |                  ID                  |
+--------------------+--------------------------------------+
| foo.bar.net.       | 1fe5c74b-e478-43a7-9ee6-5413ae080086 |
+--------------------+--------------------------------------+
| foo.sys.bar.net.   | 19e21b0a-682c-425c-a016-9cb1c5bbee32 |
+--------------------+--------------------------------------+
```

Alternatively, in place of the `--host`, `--access-key`, and `--secret-key` options, `vinyldns` will use the following environment variables:

```
VINYLDNS_HOST=
VINYLDNS_ACCESS_KEY=
VINYLDNS_SECRET_KEY=
```

### Docker

There is also a `vinyldns-cli` [Docker image](https://hub.docker.com/r/vinyldns/vinyldns-cli/).

Usage...

```
docker pull vinyldns/vinyldns-cli
```

```
docker run vinyldns/vinyldns-cli:latest --help
NAME:
   vinyldns - A CLI to the vinyldns DNS-as-a-service API

USAGE:
   vinyldns [global options] command [command options] [arguments...]

...
```

## Development

To compile, lint, run acceptance tests, etc.:

```
make
```

### Testing

The `tests` directory contains a suite of [bats](https://github.com/sstephenson/bats) acceptance tests verifying `vinyldns` commands. Tests should accompany New features.
