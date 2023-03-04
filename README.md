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

# [SAMPLE PROXIES] - [March 04 2023 | 05:50:08]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 2531
   - **SOCKS5** -> 573
   - **HTTP** -> 2457
   - **HTTPS** -> 2665

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 5751
   - **Unique Online Proxies** -> 5751
   - **Unique Online/Offline Proxies (Archive)** -> 30050

## [SOCKS4 (2531/5751)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.0.136.49:4145
1.2.214.69:4145
1.2.218.69:4145
1.4.195.114:4145
1.9.27.216:4153
1.9.164.242:35471
1.9.167.36:60489
1.9.213.114:4153
1.10.179.99:4145
1.10.251.137:4145
1.20.95.95:5678
1.20.184.75:4153
1.20.203.200:4145
1.20.207.56:4153
1.20.220.79:4145
1.20.227.66:4145
1.20.235.153:5678
1.20.250.242:4145
1.179.130.201:4153
1.179.147.5:52210
1.179.148.9:36476
1.179.148.33:1080
1.179.151.165:31948
1.179.173.114:4153
1.212.157.114:4145
3.83.234.151:8088
3.87.169.101:8088
3.141.13.98:5678
5.34.74.234:5678
5.58.66.55:14888
```

## [SOCKS5 (573/5751)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.179.220.211:59166
1.180.0.162:7302
1.180.49.222:7302
3.83.234.151:8088
3.95.212.152:8088
3.123.31.44:8443
5.78.24.0:8443
5.78.28.85:8443
5.78.31.61:8443
5.133.195.64:60230
5.135.1.146:25275
5.141.121.142:1080
5.165.7.51:1080
5.189.63.14:20996
5.189.153.171:18701
8.140.134.186:80
8.142.3.145:3306
8.210.71.234:8111
8.218.153.42:1080
8.219.156.78:1080
8.219.182.128:1080
14.23.62.59:7300
14.165.245.206:1080
15.204.140.137:17516
18.163.25.217:8080
18.166.72.199:38080
18.205.20.139:8088
23.239.4.85:59166
24.249.199.4:4145
24.249.199.12:4145
```

## [HTTP (2457/5751)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.1.220.63:8080
1.1.220.72:8080
1.2.218.69:4145
1.2.252.65:8080
1.10.141.115:8080
1.20.225.123:8080
1.85.52.250:9797
1.179.136.98:8080
1.179.144.41:8080
1.179.148.9:36476
2.58.217.1:8080
2.184.4.66:6565
2.184.4.70:6565
3.20.236.208:49205
3.84.68.97:8118
3.88.132.147:9999
3.95.212.152:8088
3.109.238.5:8080
3.215.177.148:49205
3.223.195.81:9999
3.239.195.52:9999
4.16.68.158:443
5.78.77.158:8080
5.104.174.199:23500
5.133.27.222:8080
5.158.126.16:3128
5.202.115.102:8080
5.202.191.225:8080
8.242.172.174:8080
8.242.176.198:999
```

## [HTTPS (2665/5751)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.171.213:8080
1.1.220.63:8080
1.1.220.72:8080
1.2.252.65:8080
1.10.141.115:8080
1.20.225.123:8080
1.53.252.228:2022
1.85.52.250:9797
1.179.136.98:8080
1.179.144.41:8080
1.179.148.9:36476
2.58.217.1:8080
2.184.4.66:6565
2.184.4.70:6565
3.20.236.208:49205
3.84.68.97:8118
3.87.92.76:9999
3.87.143.160:9999
3.88.132.147:9999
3.91.17.141:9999
3.109.238.5:8080
3.215.177.148:49205
3.223.195.81:9999
3.239.254.32:9999
4.16.68.158:443
5.21.66.94:8080
5.75.175.246:8080
5.75.181.164:8080
5.75.189.168:8080
5.78.31.93:8443
```

## [ARCHIVE (5751/30050)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.136.28:4145
1.0.136.49:4145
1.0.136.138:4145
1.0.136.221:4145
1.0.137.61:4153
1.0.144.43:4145
1.0.146.166:4145
1.0.150.180:4145
1.0.153.37:4145
1.0.157.96:4153
1.0.161.47:4145
1.0.162.225:4153
1.0.170.50:80
1.0.171.213:8080
1.0.205.87:8080
1.0.208.68:4145
1.0.208.177:4153
1.0.209.43:4145
1.0.213.54:4145
1.0.220.65:4145
1.0.229.192:8080
1.1.189.58:8080
1.1.220.63:8080
1.1.220.71:8080
1.1.220.72:8080
1.1.220.100:8080
1.1.230.242:4145
```



Thx Co Pure Gs - Sort Meister! 💟