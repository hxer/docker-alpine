# alpine-s6

Alpine base image with S6 copy of `root` folder. Doesn't use [go-dnsmasq](https://github.com/janeczku/go-dnsmasq) by default.

## Usage

    docker run janes/alpine-s6

## Related

[janeczku/alpine-kubernetes](https://github.com/janeczku/docker-alpine-kubernetes) - original inspration for this image came from the author of `go-dnsmasq`
[smebberson/docker-alpine](https://github.com/smebberson/docker-alpine) - another good base image using both s6 and dnsmasq. However it is almost 4mb bigger than `janeczku/alpine-kubernetes`

