<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/jetkai/proxy-list?style=flat&logo=github
[contributors-url]: https://github.com/jetkai/proxy-list/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/jetkai/proxy-list?style=flat&logo=github
[forks-url]: https://github.com/jetkai/proxy-list/network/members
[stars-shield]: https://img.shields.io/github/stars/jetkai/proxy-list?style=flat&logo=github
[stars-url]: https://github.com/jetkai/proxy-list/stargazers
[issues-shield]: https://img.shields.io/github/issues/jetkai/proxy-list?style=flat&logo=github
[issues-url]: https://github.com/jetkai/proxy-list/issues
[license-shield]: https://img.shields.io/github/license/jetkai/proxy-list?style=flat&logo=github
[license-url]: https://github.com/jetkai/proxy-list/blob/main/LICENSE
[commit-shield]: https://img.shields.io/github/last-commit/jetkai/proxy-list?style=flat&logo=github
[commit-url]: https://github.com/jetkai/proxy-list/commits/main
[commit-activity]: https://img.shields.io/github/commit-activity/w/jetkai/proxy-list?style=flat&logo=github
[commit-activity-url]: https://github.com/jetkai/proxy-list/commits/main

# 🎁 SOCKS4/5 & HTTP/S PROXIES // ONLINE + ARCHIVE

[![Commits][commit-shield]][commit-url]
[![Commits][commit-activity]][commit-activity-url]
[![Stargazers][stars-shield]][stars-url]
[![Forks][forks-shield]][forks-url]
[![Issues][issues-shield]][issues-url]

###### [ProxyScraper 1.0](https://github.com/jetkai/proxy-scraper) | `Current` Gathers a list of untested proxies from various sources `(No Setup Required - Exe/Jar Available)`
###### [ProxyBuilder 2.0](https://github.com/jetkai/proxy-builder-2) | `Current` Tests the proxies to verify they are real proxies & online
###### [ProxyBuilder 1.0](https://github.com/jetkai/ProxyBuilder) | `Old` Tests the proxies to verify they are real proxies & online

## 🔗ProxyList Links (Direct URL)

###### Classic View (IP:Port Only)

- _Online Proxies:_
[**JSON**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/json/proxies.json), [**TXT**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies.txt), [**CSV**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/csv/proxies.csv), [**XML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/xml/proxies.xml), [**YAML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/yaml/proxies.yaml)

- _Online/Offline Proxies (Archive):_
[**JSON**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/json/proxies.json), [**TXT**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt), [**CSV**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/csv/proxies.csv), [**XML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/xml/proxies.xml), [**YAML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/yaml/proxies.yaml)

###### Basic View (Without Country/Statistics)

- _Online Proxies:_
[**JSON**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/json/proxies-basic.json), [**CSV**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/csv/proxies-basic.csv), [**XML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/xml/proxies-basic.xml), [**YAML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/yaml/proxies-basic.yaml)

###### Advanced View (With Country/Statistics)
- _Online Proxies:_
[**JSON**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/json/proxies-advanced.json), [**CSV**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/csv/proxies-advanced.csv), [**XML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/xml/proxies-advanced.xml), [**YAML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/yaml/proxies-advanced.yaml)

- _Online/Offline Proxies (Archive):_
[**JSON**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/json/proxies-archive.json), [**CSV**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/csv/proxies-archive.csv), [**XML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/xml/proxies-archive.xml), [**YAML**](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/yaml/proxies-archive.yaml)

## 📰About This Project & The Proxies
This repository contains a free list of tested SOCKS4/5 & HTTP/S proxies.

#### ✔️ Free to use & for educational purposes
#### ✔️ 24/7 hourly updates (Committing since Jul-2021)
#### ✔️ Supported list formats -> JSON / TXT / CSV / XML / YAML
#### ✔️ No authentication is required when connecting any of these proxies 
#### ✔️ Only confirmed working proxies are added to these lists, including the archive

## 👩‍💻Proxy Testing

These proxies are tested every hour against EU/US hosting providers - **see below**, they have been verified to write & read data <**AT THE TIME OF TESTING**>.

**Hosting Provider**|**Country**|**Continent**
:-----:|:-----:|:-----:
OVH|France|EU
Amazon Web Services|United States|NA
Oracle Cloud|United Kingdom, Japan|EU, AS
Microsoft Azure|Hong Kong|AS

[Source Code](https://github.com/jetkai/proxy-builder-2/blob/master/src/main/kotlin/pe/proxy/proxybuilder2/net/proxy/tester/ProxyConnect.kt)
```kotlin
    //Netty4 Connect Example
    private fun connect(proxyData : ProxyChannelData) {
        val endpoint = proxyData.endpointServer ?: return
        val awaitTime = (if(pause.get()) 30000 else config.connectAwait)

        Bootstrap().group(workerGroup)
            .channel(NioSocketChannel::class.java)
            .resolver(NoopAddressResolverGroup.INSTANCE)
            .option(ChannelOption.AUTO_READ, proxyData.autoRead)
            .option(ChannelOption.TCP_NODELAY, true)
            .option(ChannelOption.CONNECT_TIMEOUT_MILLIS, config.timeout)
            .handler(ProxyChannelInitializer(proxyData))
            .connect(InetSocketAddress(endpoint.ip, endpoint.port))
            .channel().closeFuture().awaitUninterruptibly(awaitTime)
    }
```

## 🕵️Proxy Detection, Risk & Geolocation

###### Proxy Detection/Risk is provided by [ProxyCheck.io - API](https://proxycheck.io/)

###### Geolocation is provided by [GeoLite2 country database](https://www.maxmind.com)

<img src="https://user-images.githubusercontent.com/26250917/219546484-78aed231-c28f-4d0a-8fb5-a0dd22cf8bc1.png" width="75%">


## 📝Proxy Formatting

These proxies are scraped from various sources ([ProxyScraper](https://github.com/jetkai/proxy-scraper)) & I compile this data using my [ProxyBuilder](https://github.com/jetkai/proxy-builder-2) application. 

Proxies are sorted from lowest to highest 0-255 & duplicated proxies are removed — the only exception is if an IP has a different port open, which is also a working proxy tunnel <**Less than 1% of the total proxies at the time of testing**>.

```IP:Port -> 1.0.132.249:4153```

## ✔Compatability

These proxies should work for any application that can establish an HTTP, HTTPS, SOCKS4 or SOCKS5 connection. Such as, an application that has proxy support (FireFox, Chrome), or as an example, these Java Apps below. 

- [JaySyiPker](https://github.com/JayArrowz/JaySyiPker)
- [Bruteforce-RSPS](https://github.com/jetkai/Bruteforce-RSPS)
- [718 Cheat Client (Final)](https://github.com/jetkai/718-Cheat-Client-Final)

---

# [SAMPLE PROXIES] - [April 06 2023 | 06:50:08]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 1853
   - **SOCKS5** -> 1257
   - **HTTP** -> 2210
   - **HTTPS** -> 2768

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 6091
   - **Unique Online Proxies** -> 6091
   - **Unique Online/Offline Proxies (Archive)** -> 44998

## [SOCKS4 (1853/6091)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.0.163.158:4145
1.4.195.114:4145
1.4.247.1:4153
1.9.164.242:35471
1.9.167.35:60489
1.9.167.36:60489
1.20.95.95:5678
1.20.137.82:32241
1.20.227.66:4145
1.32.57.85:5678
1.53.137.84:4145
1.120.134.30:5678
1.179.130.201:4153
1.179.147.5:52210
1.179.148.9:36476
1.212.157.114:4145
1.221.173.148:4145
3.141.13.98:5678
5.8.240.90:4153
5.8.240.92:4153
5.22.154.50:32127
5.34.74.234:5678
5.58.47.25:3629
5.128.254.99:1080
5.133.30.68:5678
5.141.87.135:3629
5.152.235.251:5615
5.160.61.122:4145
5.178.204.235:2082
5.226.125.10:10801
```

## [SOCKS5 (1257/6091)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.180.0.162:7302
3.84.184.94:8088
5.56.124.176:8192
5.128.254.99:1080
5.165.7.51:1080
5.189.97.62:1080
5.189.159.215:59166
8.142.3.145:3306
8.210.71.234:8111
8.210.253.223:53854
8.218.160.143:1080
18.163.25.217:8080
18.166.72.199:38080
18.205.19.148:8088
18.206.168.5:8088
20.205.59.85:1080
24.249.199.4:4145
24.249.199.12:4145
31.25.24.67:1080
31.41.90.142:1080
31.43.203.100:1080
31.45.237.66:8192
31.172.67.97:443
31.211.130.237:8192
31.217.221.74:8192
36.93.9.178:1080
37.18.73.94:5566
37.44.238.2:54140
37.60.141.236:8192
37.144.205.159:7788
```

## [HTTP (2210/6091)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.1.220.63:8080
1.1.220.71:8080
1.9.83.210:1337
1.10.141.115:8080
1.20.225.123:8080
1.85.52.250:9797
1.179.136.98:8080
1.179.148.9:36476
2.58.217.1:8080
3.84.184.94:8088
3.87.27.64:8118
3.89.73.90:8118
3.95.65.32:9999
3.215.177.148:49205
4.16.68.158:443
5.2.75.58:8118
5.56.92.25:8090
5.78.43.251:8080
5.78.80.33:8080
5.78.87.122:8080
5.78.88.230:8080
5.78.99.34:8080
5.78.99.40:8080
5.78.99.44:8080
5.78.99.48:8080
5.78.99.54:8080
5.78.99.56:8080
5.78.102.192:8080
5.78.102.193:8080
5.78.103.75:8080
```

## [HTTPS (2768/6091)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.171.213:8080
1.1.220.63:8080
1.1.220.71:8080
1.9.83.210:1337
1.10.141.115:8080
1.20.225.123:8080
1.53.252.228:2022
1.85.52.250:9797
1.179.136.98:8080
1.179.148.9:36476
2.58.217.1:8080
2.138.28.204:3128
3.87.27.64:8118
3.111.55.27:80
3.215.177.148:49205
4.16.68.158:443
5.8.53.7:18081
5.75.167.72:8080
5.78.40.118:8080
5.78.40.220:8080
5.78.41.44:8080
5.78.42.130:8080
5.78.43.36:8080
5.78.43.180:8080
5.78.43.238:8080
5.78.45.160:8080
5.78.45.172:8080
5.78.46.5:8080
5.78.46.235:8080
5.78.64.58:8080
```

## [ARCHIVE (6091/44998)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.136.28:4145
1.0.136.49:4145
1.0.136.138:4145
1.0.136.221:4145
1.0.137.61:4153
1.0.141.70:8080
1.0.141.132:8080
1.0.144.43:4145
1.0.146.166:4145
1.0.150.180:4145
1.0.153.37:4145
1.0.157.96:4153
1.0.160.29:4145
1.0.160.38:4145
1.0.161.47:4145
1.0.161.232:4145
1.0.162.225:4153
1.0.163.158:4145
1.0.170.50:80
1.0.171.213:8080
1.0.205.87:8080
1.0.208.68:4145
1.0.208.108:4145
1.0.208.111:4145
1.0.208.131:4145
1.0.208.177:4153
1.0.208.231:4145
```



Thx Co Pure Gs - Sort Meister! 💟