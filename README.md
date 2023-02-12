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

###### Major update -> 29/05/2022 | [ProxyBuilder 2.0](https://github.com/jetkai/proxy-builder-2)
###### Previous version -> 22/07/2021 - 28/05/2022 | [ProxyBuilder 1.0](https://github.com/jetkai/ProxyBuilder)

## 📰About This Project & The Proxies
This repository contains a free list of tested SOCKS4/5 & HTTP/S proxies in -> **JSON**, **TXT**, **CSV**, **XML** & **YAML** format. No authentication is required when connecting to these proxies.

## 👩‍💻Proxy Testing

These proxies are tested ~12x/day (every 2 hours) against EU/US hosting providers - **see below**, they have been verified to write & read data <**AT THE TIME OF TESTING**>.

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

## 📝Proxy Formatting

These proxies are scraped from various sources & I compile this data using my [ProxyBuilder](https://github.com/jetkai/ProxyBuilder) application. Proxies are sorted from lowest to highest 0-255 & duplicated proxies are removed — the only exception is if an IP has a different port open, which is also a working proxy tunnel <**Less than 1% of the total proxies at the time of testing**>.

```IP:Port -> 1.0.132.249:4153```

## ✔Compatability

These proxies should work for any application that can establish an HTTP, HTTPS, SOCKS4 or SOCKS5 connection. Such as, an application that has proxy support (FireFox, Chrome), or as an example, these Java Apps below. 

- [JaySyiPker](https://github.com/JayArrowz/JaySyiPker)
- [Bruteforce-RSPS](https://github.com/jetkai/Bruteforce-RSPS)
- [718 Cheat Client (Final)](https://github.com/jetkai/718-Cheat-Client-Final)

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

---

# [SAMPLE PROXIES] - [February 12 2023 | 05:12:40]

### Proxy Statistics:
- _Online Proxies (By Protocol):_
   - **SOCKS4** -> 748
   - **SOCKS5** -> 222
   - **HTTP** -> 547
   - **HTTPS** -> 482

- _Proxies (Total):_
   - **Online Proxies (SOCKS4/5 + HTTP/S)** -> 1302
   - **Unique Online Proxies** -> 1302
   - **Unique Online/Offline Proxies (Archive)** -> 13244

## [SOCKS4 (748/1302)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks4.txt)
```yaml
1.9.167.36:60489
1.20.95.95:5678
1.32.57.85:5678
1.32.59.217:47045
1.179.148.9:36476
1.221.173.148:4145
3.131.207.170:13343
3.141.13.98:5678
5.22.154.50:32127
5.58.33.187:55507
5.58.53.216:1085
5.135.1.146:25275
5.178.217.227:31019
5.188.64.79:5678
5.189.153.171:18701
8.17.28.139:39593
8.39.228.161:39593
8.42.68.197:39593
8.134.136.224:8080
8.134.138.108:443
8.136.192.43:80
8.208.90.243:1234
8.209.240.66:9999
8.209.249.96:3128
8.209.253.237:9999
8.213.128.90:9999
8.213.129.20:3080
8.213.137.155:8084
8.219.43.134:9002
8.219.167.110:443
```

## [SOCKS5 (222/1302)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-socks5.txt)
```yaml
1.180.0.162:7302
3.131.207.170:13343
8.134.136.224:8080
8.134.139.219:3128
8.136.192.43:80
8.208.85.34:3128
8.208.89.32:1234
8.208.90.194:8064
8.209.249.96:3128
8.209.253.237:9999
8.213.129.15:8989
8.213.137.155:8084
8.219.5.240:443
8.219.43.134:9002
8.219.74.58:1234
20.239.2.157:80
24.249.199.4:4145
24.249.199.12:4145
31.43.203.100:1080
31.202.25.190:3128
31.210.52.150:59166
37.18.73.60:5566
39.104.57.170:3333
39.104.62.128:81
43.128.36.71:3389
45.119.83.197:5664
45.148.121.228:443
46.232.121.130:1145
47.74.64.65:9002
47.74.226.8:5001
```

## [HTTP (547/1302)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-http.txt)
```yaml
1.0.170.50:80
1.1.189.58:8080
1.32.59.217:47045
1.179.144.41:8080
1.179.148.9:36476
3.20.236.208:49205
3.215.177.148:49205
5.44.62.166:8080
5.58.33.187:55507
5.180.130.90:80
12.88.29.66:9080
12.144.254.185:9080
14.170.154.10:8080
14.177.236.212:55443
18.216.72.10:5678
18.222.17.49:49205
24.172.34.114:49920
24.172.82.94:53281
31.43.52.176:41890
31.46.33.59:53281
31.161.38.233:8090
34.229.130.62:49205
34.230.89.25:49205
36.67.11.41:8080
36.67.27.189:39674
36.67.237.146:3128
36.89.212.251:8080
36.89.212.252:8080
36.89.229.97:50540
36.92.70.209:8080
```

## [HTTPS (482/1302)](https://raw.githubusercontent.com/jetkai/proxy-list/main/online-proxies/txt/proxies-https.txt)
```yaml
1.0.170.50:80
1.1.189.58:8080
1.32.59.217:47045
1.179.144.41:8080
1.179.148.9:36476
3.20.236.208:49205
3.215.177.148:49205
5.44.62.166:8080
5.58.33.187:55507
5.180.130.90:80
12.88.29.66:9080
12.144.254.185:9080
14.170.154.10:8080
14.177.236.212:55443
18.216.72.10:5678
18.222.17.49:49205
24.172.34.114:49920
24.172.82.94:53281
31.43.52.176:41890
31.46.33.59:53281
31.161.38.233:8090
34.229.130.62:49205
34.230.89.25:49205
36.67.11.41:8080
36.67.27.189:39674
36.67.237.146:3128
36.89.212.251:8080
36.89.212.252:8080
36.89.229.97:50540
36.92.70.209:8080
```

## [ARCHIVE (1302/13244)](https://raw.githubusercontent.com/jetkai/proxy-list/main/archive/txt/proxies.txt)
```yaml
1.0.132.249:4153
1.0.133.89:4153
1.0.133.100:51327
1.0.137.61:4153
1.0.170.50:80
1.0.205.87:8080
1.1.189.58:8080
1.1.220.100:8080
1.2.252.65:8080
1.4.157.35:36202
1.4.195.114:4145
1.4.214.148:5678
1.9.164.242:35471
1.9.167.35:60489
1.9.167.36:60489
1.9.213.114:4153
1.10.133.211:4145
1.10.140.43:4145
1.10.141.220:54620
1.10.189.133:50855
1.20.95.95:5678
1.20.96.30:4153
1.20.96.164:4153
1.20.137.82:32241
1.20.166.142:8080
1.20.169.235:8080
1.20.184.75:4153
1.20.209.28:8080
1.20.217.52:8080
1.20.220.79:4145
```



Thx Co Pure Gs - Sort Meister! 💟