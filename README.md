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

# [SAMPLE PROXIES] - [April 12 2023 | 04:50:09]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 1272
   - **SOCKS5** -> 281
   - **HTTP** -> 1289
   - **HTTPS** -> 1552

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 3213
   - **Unique Online Proxies** -> 3213
   - **Unique Online/Offline Proxies (Archive)** -> 47845

## [SOCKS4 (1272/3213)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.2.214.69:4145
1.9.164.242:35471
1.9.167.35:60489
1.20.184.75:4153
1.20.227.66:4145
1.179.130.201:4153
2.57.131.19:4145
2.135.223.134:5678
5.58.47.25:3629
5.141.87.135:3629
5.178.204.235:2082
5.178.217.227:31019
5.180.19.209:1080
8.39.228.35:39593
8.210.200.44:5555
12.11.59.114:1080
12.109.102.86:64312
12.131.183.66:30504
13.58.88.184:5678
13.58.223.158:5678
14.97.130.222:5678
14.160.23.139:4145
14.161.14.106:5678
14.207.6.40:5678
18.206.212.30:8088
24.75.156.114:3366
24.88.66.70:64312
24.234.142.118:31008
24.249.199.4:4145
24.249.199.12:4145
```

## [SOCKS5 (281/3213)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.180.0.162:7302
3.239.64.123:8088
5.180.19.209:1080
8.142.3.145:3306
8.210.63.102:55380
8.210.253.223:53854
8.218.160.143:1080
18.163.25.217:8080
24.249.199.4:4145
24.249.199.12:4145
31.45.237.66:8192
31.211.130.237:8192
31.217.221.74:8192
34.79.91.3:59040
37.44.238.2:54140
37.60.141.236:8192
37.193.40.16:1080
39.170.85.129:7302
39.187.67.196:1080
42.193.240.65:80
45.32.114.246:8081
45.55.32.201:36353
46.10.208.106:8192
46.251.9.238:8192
47.243.95.228:10080
51.68.139.131:31609
51.75.74.195:7497
51.77.99.180:443
51.178.82.49:59166
51.178.141.208:42554
```

## [HTTP (1289/3213)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.9.83.210:1337
1.10.141.115:8080
1.20.225.123:8080
1.85.52.250:9797
3.20.236.208:49205
3.87.27.64:8118
3.128.178.229:9090
3.208.1.201:9999
3.215.177.148:49205
3.236.171.143:9999
4.16.68.158:443
5.9.118.41:8889
5.58.97.89:8080
5.158.126.16:3128
8.135.48.42:8080
8.242.150.91:999
8.242.190.125:999
14.102.13.161:8080
14.102.51.185:8080
14.161.27.174:8080
14.161.33.150:8080
14.241.62.111:19132
14.241.111.38:8080
24.164.58.61:32650
24.230.33.96:3128
27.42.168.46:61308
27.71.248.123:8080
27.72.244.228:8080
27.147.209.215:8080
31.28.8.196:9898
```

## [HTTPS (1552/3213)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.171.213:8080
1.9.83.210:1337
1.10.141.115:8080
1.20.169.79:8080
1.20.225.123:8080
1.53.252.228:2022
1.85.52.250:9797
2.50.153.194:53281
2.138.28.204:3128
3.20.236.208:49205
3.87.27.64:8118
3.93.183.112:9999
3.111.55.27:80
3.112.27.164:8118
3.208.1.201:9999
3.215.177.148:49205
3.236.171.143:9999
4.16.68.158:443
5.58.97.89:8080
5.78.92.68:50001
5.158.126.16:3128
5.160.101.234:8080
5.161.110.95:50001
5.161.180.82:50001
8.135.48.42:8080
8.219.6.87:3311
8.219.176.202:8080
8.242.178.3:999
8.242.190.125:999
14.20.235.216:808
```

## [ARCHIVE (3213/47845)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.136.28:4145
1.0.136.49:4145
1.0.136.99:4145
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
```



Thx Co Pure Gs - Sort Meister! 💟