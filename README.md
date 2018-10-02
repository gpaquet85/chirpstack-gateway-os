# LoRa Gateway OS

The LoRa Gateway OS is an embedded OS for LoRa gateways. It is part of the
open-source [LoRa Server project](https://www.loraserver.io/).

The goal of the LoRa Gateway OS is to provide firmware images that are easy
to setup, maintain and customize.

## Images

### lora-gateway-os-base

Provides the following features:

* [Monit](https://mmonit.com/monit/) based service monitoring
* Semtech [packet-forwarder](https://github.com/lora-net/packet_forwarder)
* [LoRa Gateway Bridge](https://github.com/brocaar/lora-gateway-bridge/)

## Targets

* Raspberry Pi 3
    * [RAK - RAK381 Gateway Developer Kit](https://www.rakwireless.com/en/WisKeyOSH/RAK831)
    * [IMST - iC880A](https://wireless-solutions.de/products/long-range-radio/ic880a.html)
	* [RisingHF - RHF0M301 LoRaWAN IoT Discovery Kit](http://risinghf.com/#/product-details?product_id=9&lang=en)

## Using

### Login

The default username is `admin` with password `admin`.

### Gateway configuration

Execute the following command as `admin` user:

```bash
sudo gateway-config
```

## Building images

A Docker based build environment is provided for compiling the images.

### Initial setup

Run the following command to set the `/build` folder permissions:

```bash
# on the host
docker-compose run --rm busybox

# within the container
chown 999:999 /build
```

### Building

Run the following command to setup the build environment:

```bash
# on the host
docker-compose run --rm yocto bash

# within the container

# update the submodules
make submodules

# initialize the yocto / openembedded build environment
source oe-init-build-env /build/ /lora-gateway-os/bitbake/


# build the lora-gateway-os-base image
bitbake lora-gateway-os-base
```

#### Configuration

By default, Raspberry Pi3 is configured as the target platform. You need to
update the following configuration files to configure a different target:

* `/build/config/local.conf`
* `/build/config/bblayers.conf`

