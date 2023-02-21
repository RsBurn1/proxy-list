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

# [SAMPLE PROXIES] - [February 21 2023 | 07:50:07]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 2190
   - **SOCKS5** -> 1233
   - **HTTP** -> 2442
   - **HTTPS** -> 2495

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 5085
   - **Unique Online Proxies** -> 5085
   - **Unique Online/Offline Proxies (Archive)** -> 22297

## [SOCKS4 (2190/5085)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.0.0.12:80
1.0.0.46:80
1.0.0.57:80
1.0.0.66:80
1.0.0.98:80
1.0.0.128:80
1.0.0.135:80
1.0.0.156:80
1.1.1.100:80
1.1.1.154:80
1.1.1.206:80
1.4.195.114:4145
1.9.164.242:35471
1.9.167.36:60489
1.9.213.114:4153
1.20.95.95:5678
1.20.168.24:4145
1.20.227.66:4145
1.53.137.84:4145
1.116.243.147:9999
1.179.148.9:36476
1.179.151.165:31948
1.179.173.114:4153
1.214.62.71:8000
1.221.173.148:4145
2.135.223.134:5678
3.0.28.197:80
3.73.143.2:80
3.73.199.227:80
3.85.7.155:8083
```

## [SOCKS5 (1233/5085)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.0.0.33:80
1.0.0.65:80
1.0.0.134:80
1.0.0.153:80
1.0.0.197:80
1.0.0.214:80
1.1.1.159:80
1.1.1.182:80
1.1.1.229:80
1.179.112.1:80
1.179.220.211:59166
1.180.0.162:7302
1.214.62.71:8000
1.234.45.130:80
3.73.143.2:80
3.73.199.227:80
3.85.7.155:8083
3.221.105.1:80
3.237.253.189:8088
5.9.112.247:3128
5.9.113.60:9000
5.23.54.72:59166
5.78.30.74:8443
5.78.31.61:8443
5.135.188.61:2082
5.141.121.142:1080
5.165.7.51:1080
5.180.181.26:8888
5.181.252.102:59166
5.189.130.207:46257
```

## [HTTP (2442/5085)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.0.205.87:8080
1.1.189.58:8080
1.1.220.63:8080
1.1.220.100:8080
1.10.141.115:8080
1.10.231.42:8080
1.85.52.250:9797
1.179.136.98:8080
1.179.148.9:36476
1.214.62.71:8000
3.20.236.208:49205
3.85.7.155:8083
3.109.238.5:8080
3.215.177.148:49205
4.16.68.158:443
4.59.83.198:8080
5.9.112.247:3128
5.9.149.118:40000
5.16.13.48:8080
5.53.16.185:18080
5.58.58.209:8080
5.58.105.135:3128
5.104.174.199:23500
5.160.243.238:8080
5.163.121.114:8080
5.180.33.23:1337
5.180.130.90:80
5.180.130.91:8080
5.195.40.27:8080
8.130.34.44:8118
```

## [HTTPS (2495/5085)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.205.87:8080
1.1.189.58:8080
1.1.220.63:8080
1.1.220.100:8080
1.10.141.115:8080
1.10.231.42:8080
1.20.169.59:8080
1.85.52.250:9797
1.179.136.98:8080
1.179.148.9:36476
1.214.62.71:8000
3.20.236.208:49205
3.85.7.155:8083
3.109.238.5:8080
3.111.55.27:80
3.215.177.148:49205
4.16.68.158:443
4.59.83.198:8080
5.9.112.247:3128
5.9.149.118:40000
5.16.13.48:8080
5.53.16.185:18080
5.58.58.209:8080
5.58.105.135:3128
5.75.129.196:8080
5.75.151.243:8080
5.75.230.117:8080
5.75.249.77:8080
5.78.73.73:8080
5.78.81.188:8080
```

## [ARCHIVE (5085/22297)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.0.12:80
1.0.0.33:80
1.0.0.46:80
1.0.0.57:80
1.0.0.65:80
1.0.0.66:80
1.0.0.98:80
1.0.0.128:80
1.0.0.134:80
1.0.0.135:80
1.0.0.153:80
1.0.0.156:80
1.0.0.197:80
1.0.0.214:80
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.136.221:4145
1.0.137.61:4153
1.0.150.180:4145
1.0.161.47:4145
1.0.170.50:80
1.0.205.87:8080
1.0.213.54:4145
1.0.229.192:8080
1.1.1.100:80
1.1.1.154:80
1.1.1.159:80
1.1.1.182:80
1.1.1.206:80
```



Thx Co Pure Gs - Sort Meister! 💟