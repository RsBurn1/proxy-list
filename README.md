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

# [SAMPLE PROXIES] - [April 03 2023 | 08:50:08]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 1657
   - **SOCKS5** -> 377
   - **HTTP** -> 2203
   - **HTTPS** -> 2713

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 5037
   - **Unique Online Proxies** -> 5037
   - **Unique Online/Offline Proxies (Archive)** -> 41199

## [SOCKS4 (1657/5037)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.4.195.114:4145
1.9.164.242:35471
1.9.167.35:60489
1.9.213.114:4153
1.10.251.36:4145
1.20.95.95:5678
1.20.220.79:4145
1.20.235.153:5678
1.32.57.85:5678
1.53.137.84:4145
1.179.148.9:36476
1.179.148.33:1080
1.179.151.165:31948
3.141.13.98:5678
5.8.240.90:4153
5.34.74.234:5678
5.44.254.40:4145
5.58.66.55:14888
5.133.30.68:5678
5.135.1.146:25275
5.141.87.135:3629
5.152.235.251:5615
5.178.204.235:2082
5.178.217.227:31019
5.188.64.79:5678
8.39.228.33:39593
8.39.228.193:39593
8.42.68.93:39593
8.210.200.44:5555
12.11.59.114:1080
```

## [SOCKS5 (377/5037)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.180.0.162:7302
3.84.184.94:8088
3.91.189.187:8088
5.11.17.230:1080
5.56.124.176:8192
5.135.1.146:25275
5.165.7.51:1080
5.189.97.62:1080
8.210.253.223:53854
8.218.160.143:1080
14.23.62.59:7300
18.163.25.217:8080
20.205.59.85:1080
24.249.199.4:4145
24.249.199.12:4145
27.79.66.154:5209
31.43.203.100:1080
31.45.237.66:8192
31.172.67.97:443
31.202.25.190:3128
31.211.130.237:8192
36.6.145.170:8089
37.18.73.94:5566
37.60.141.236:8192
37.187.153.227:54988
37.252.1.145:34918
38.240.49.245:6500
39.104.208.49:80
39.170.85.129:7302
43.132.238.17:24018
```

## [HTTP (2203/5037)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.0.205.87:8080
1.1.220.63:8080
1.4.214.178:8080
1.4.250.146:8080
1.9.83.210:1337
1.20.225.123:8080
1.85.52.250:9797
1.179.148.9:36476
2.184.4.69:6565
3.20.236.208:49205
3.84.68.97:8118
3.84.184.94:8088
3.87.27.64:8118
3.128.178.229:9090
3.215.177.148:49205
4.16.68.158:443
5.2.228.168:8888
5.9.118.41:8889
5.56.92.25:8090
5.78.44.242:8080
5.78.70.54:8080
5.78.100.18:8080
5.104.174.199:23500
5.133.31.74:8080
5.158.126.16:3128
5.160.175.226:8383
5.202.103.100:514
5.202.191.225:8080
8.135.48.42:8080
8.242.172.56:1994
```

## [HTTPS (2713/5037)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.141.132:8080
1.0.171.213:8080
1.0.205.87:8080
1.1.220.63:8080
1.9.83.210:1337
1.10.253.88:8080
1.20.169.20:8080
1.20.225.123:8080
1.85.52.250:9797
1.179.148.9:36476
3.20.236.208:49205
3.84.68.97:8118
3.84.204.82:9999
3.87.27.64:8118
3.215.177.148:49205
4.16.68.158:443
5.8.53.7:18081
5.75.135.217:8080
5.75.141.69:8080
5.75.143.44:8080
5.75.145.233:8080
5.75.159.173:8080
5.75.160.177:8080
5.75.173.70:8080
5.75.224.218:8080
5.75.233.30:8080
5.75.234.253:8080
5.78.43.153:8080
5.78.44.63:8080
5.78.66.155:8080
```

## [ARCHIVE (5037/41199)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
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
1.0.160.38:4145
1.0.161.47:4145
1.0.161.232:4145
1.0.162.225:4153
1.0.170.50:80
1.0.171.213:8080
1.0.205.87:8080
1.0.208.68:4145
1.0.208.108:4145
1.0.208.111:4145
1.0.208.131:4145
1.0.208.177:4153
1.0.208.231:4145
1.0.209.43:4145
1.0.209.129:8080
```



Thx Co Pure Gs - Sort Meister! 💟