## some safe tool

* python 
* git 
* curl
* nmap

* sqlmap
* [subDomainsBrute](https://github.com/lijiejie/subDomainsBrute)
* [dirsearch](https://github.com/maurosoria/dirsearch)
* [BruteX](https://github.com/1N3/BruteX) -- not yet to add

## run

`docker run -it janes/alpine-safetool /bin/sh`

## tool

* subDomainBrute

子域名爆破， 通过`字典`查询公共DNS服务器爆破

* dirsearch

网站目录爆破，支持php,asp等，通过`字典`爆破

* BruteX

> install.sh base on the linux, which support ap-get install, kali is best

自动爆破目标服务器上的一些服务，包括开放的端口，域名，用户名和密码

| 服务 | 检测引擎 |
| --- | ---- |
| ports | nmap |
| username/password | hydra |
| domain | dnsenum |
