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

# [SAMPLE PROXIES] - [April 13 2023 | 11:50:08]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 1455
   - **SOCKS5** -> 288
   - **HTTP** -> 1553
   - **HTTPS** -> 1842

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 3753
   - **Unique Online Proxies** -> 3753
   - **Unique Online/Offline Proxies (Archive)** -> 48134

## [SOCKS4 (1455/3753)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.0.136.99:4145
1.4.214.148:5678
1.9.164.242:35471
1.9.167.36:60489
1.10.231.237:4145
1.20.220.79:4145
1.20.227.66:4145
1.32.57.85:5678
1.179.148.9:36476
1.179.173.114:4153
1.221.173.148:4145
2.137.22.94:4153
3.141.13.98:5678
5.8.240.90:4153
5.8.240.94:4153
5.22.154.50:32127
5.34.74.234:5678
5.58.47.25:3629
5.58.66.55:14888
5.133.24.210:1080
5.135.191.56:56750
5.141.87.135:3629
5.160.61.122:4145
5.188.64.79:5678
8.39.228.35:39593
8.210.23.233:5555
12.11.59.114:1080
12.109.102.86:64312
12.131.183.66:30504
13.58.88.184:5678
```

## [SOCKS5 (288/3753)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
5.135.191.56:56750
8.142.3.145:3306
8.210.63.102:55380
8.210.253.223:53854
18.163.25.217:8080
23.253.253.26:59166
24.249.199.4:4145
24.249.199.12:4145
31.44.6.148:9100
31.45.237.66:8192
36.93.9.178:1080
37.187.153.227:54988
38.127.179.212:12436
39.170.85.129:7302
42.193.240.65:80
43.132.238.17:24018
44.202.62.60:8088
45.32.114.246:8081
45.55.32.201:36353
45.76.32.8:1080
46.10.208.106:8192
46.105.105.223:9066
47.88.104.126:3344
47.242.164.162:52686
47.243.95.228:10080
50.17.127.34:8088
51.68.94.167:29707
51.68.139.131:31609
51.75.74.195:7497
51.75.126.150:47432
```

## [HTTP (1553/3753)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.1.189.58:8080
1.2.252.65:8080
1.9.83.210:1337
1.10.141.115:8080
1.10.231.237:4145
1.85.52.250:9797
1.179.148.9:36476
2.58.217.1:8080
3.20.236.208:49205
3.128.178.229:9090
3.236.171.143:9999
4.16.68.158:443
5.2.75.58:8118
5.56.92.25:8090
5.58.97.89:8080
5.133.27.222:8080
5.160.175.226:8383
5.187.9.10:8080
8.135.48.42:8080
8.210.202.74:8118
8.242.172.174:8080
8.242.176.198:999
8.242.190.122:999
8.242.190.125:999
8.242.205.41:9991
12.36.95.132:8080
12.88.29.66:9080
12.144.254.185:9080
14.102.51.185:8080
14.143.231.22:8080
```

## [HTTPS (1842/3753)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.171.213:8080
1.1.189.58:8080
1.2.252.65:8080
1.9.83.210:1337
1.10.141.115:8080
1.20.169.132:8080
1.53.0.2:8080
1.85.52.250:9797
1.179.148.9:36476
2.50.153.194:53281
2.58.217.1:8080
2.138.28.204:3128
3.20.236.208:49205
3.93.183.112:9999
3.94.253.49:8118
3.236.171.143:9999
4.16.68.158:443
5.8.53.7:18081
5.54.186.76:8080
5.58.97.89:8080
5.78.42.62:50001
5.78.66.235:8080
5.78.81.163:8080
5.78.92.68:50001
5.78.92.135:50001
5.133.27.222:8080
5.160.175.226:8383
5.161.110.95:50001
5.161.180.82:50001
5.187.9.10:8080
```

## [ARCHIVE (3753/48134)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.136.16:4153
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
```



Thx Co Pure Gs - Sort Meister! 💟