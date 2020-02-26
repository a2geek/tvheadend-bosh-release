# Tvheadend BOSH Release

[![GitHub release](https://img.shields.io/github/v/release/a2geek/tvheadend-bosh-release)](https://github.com/a2geek/tvheadend-bosh-release/releases/latest)

This is a BOSH Release to deploy [Tvheadend](https://tvheadend.org/).

## Status

Works! Minor configuration capabilities, as most configuration seems to be in the user interface.

# Deployment

```
git clone https://github.com/a2geek/tvheadend-bosh-release.git
cd tvheadend-bosh-release
bosh -d tvheadend deploy manifest.yml
```

## Configuration options

| Operations File | Description |
| --- | --- |
| `operations/set-disk-size.yml` | Used to set a different disk size from the arbitratily chosen size of 10GiB. |

## Configuration variables

Structured variables will be similar to this:

```
tvheadend:
  disk_size: ...
  base_url: http(s)://...
```

## HDHomeRun

Note that HDHomeRun devices aren't easily discoverable. There is a companion project, [hdhomerun-discover-relay](https://github.com/a2geek/hdhomerun-discover-relay), to relay the discovery network packets out to the broader network.

Additionally, incoming packets may need help. [This advice](https://www.mythtv.org/wiki/Silicondust_HDHomeRun_Dual#Can.27t_Connect_to_HDHR.3F) was useful.  The HDHomeRun MAC address is printed on the device, and also available at the device system page (something like `http://<hdhomerun-ip-addr>/system.html`).

> Note: With the latest update, the HDHomeRun link may be really easy: http://hdhomerun.local/system.html

## Post-deployment

Note that post deployment, Tvheadend still needs to be setup. The user-interface will be at `http://<tvheadend-ip-addr>:9981`.

# Development

For those used to `make` the delete/deploy sequences are just:

```
make rmdev dev
```

Otherwise, the usual mechanisms:

```
cd tvheadend-bosh-release
bosh create-release --force
bosh upload-release
bosh -d tvheadend deploy manifest.yml -o operations/use-latest-dev.yml
```
