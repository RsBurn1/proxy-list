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

# [SAMPLE PROXIES] - [April 08 2023 | 10:50:08]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 1922
   - **SOCKS5** -> 420
   - **HTTP** -> 1895
   - **HTTPS** -> 2261

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 4832
   - **Unique Online Proxies** -> 4832
   - **Unique Online/Offline Proxies (Archive)** -> 46769

## [SOCKS4 (1922/4832)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.4.195.114:4145
1.4.214.148:5678
1.4.247.1:4153
1.9.27.212:4153
1.9.164.242:35471
1.9.167.35:60489
1.9.167.36:60489
1.9.213.114:4153
1.10.231.204:4145
1.10.253.116:4145
1.20.184.75:4153
1.20.227.66:4145
1.32.57.85:5678
1.120.134.30:5678
1.179.148.9:36476
1.179.148.33:1080
1.179.151.165:31948
1.212.157.114:4145
1.221.173.148:4145
2.135.223.134:5678
2.137.22.94:4153
3.87.169.101:8088
3.94.123.123:8088
3.141.13.98:5678
5.8.240.92:4153
5.8.240.94:4153
5.58.47.25:3629
5.58.66.55:14888
5.135.1.146:25275
5.141.87.135:3629
```

## [SOCKS5 (420/4832)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.180.0.162:7302
1.180.49.222:7302
5.56.124.176:8192
5.78.101.8:8080
5.135.1.146:25275
5.161.101.203:8080
5.189.159.215:59166
5.252.161.63:34463
8.142.3.145:3306
8.219.6.91:80
8.219.167.24:80
8.222.240.242:80
8.222.246.23:80
8.222.246.25:80
18.163.25.217:8080
18.166.72.199:38080
24.249.199.4:4145
24.249.199.12:4145
31.41.90.142:1080
31.45.237.66:8192
31.202.25.190:3128
31.207.45.123:1080
31.211.130.237:8192
31.217.221.74:8192
37.44.238.2:54140
37.60.141.236:8192
37.187.153.227:54988
37.221.193.221:13233
37.230.114.48:1081
39.104.208.49:80
```

## [HTTP (1895/4832)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.0.170.50:80
1.0.205.87:8080
1.4.214.178:8080
1.20.225.123:8080
1.85.52.250:9797
1.179.148.9:36476
2.58.217.1:8080
3.20.236.208:49205
3.87.27.64:8118
3.89.73.90:8118
3.95.65.32:9999
3.215.177.148:49205
4.16.68.158:443
5.9.118.41:8889
5.104.174.199:23500
5.146.106.57:3128
5.158.126.16:3128
5.160.175.226:8383
5.187.9.10:8080
8.242.150.91:999
8.242.176.198:999
8.242.205.41:9991
8.242.207.202:8080
12.88.29.66:9080
12.218.209.130:13326
14.29.108.150:8998
14.102.51.185:8080
14.161.26.100:8080
14.170.154.193:19132
14.207.148.111:8080
```

## [HTTPS (2261/4832)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.170.50:80
1.0.205.87:8080
1.20.225.123:8080
1.85.52.250:9797
1.179.148.9:36476
2.50.153.194:53281
2.58.217.1:8080
3.20.236.208:49205
3.85.34.96:9999
3.87.27.64:8118
3.88.208.242:9999
3.215.177.148:49205
4.16.68.158:443
5.8.53.7:18081
5.75.141.69:8080
5.75.190.15:8080
5.78.43.15:8080
5.78.43.23:8080
5.78.64.217:8080
5.78.65.154:8080
5.78.66.127:8080
5.78.67.98:8080
5.78.68.156:8080
5.78.68.196:8080
5.78.71.192:8080
5.78.73.61:8080
5.78.75.64:8080
5.78.76.224:8080
5.78.77.147:8080
5.78.78.180:8080
```

## [ARCHIVE (4832/46769)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
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