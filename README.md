# ESurfingDialer
[![GitHub License](https://img.shields.io/github/license/Rsplwe/ESurfingDialer?style=flat-square)](https://github.com/Rsplwe/ESurfingDialer/blob/main/LICENSE)

广东电信天翼校园（ZSM验证）登入认证客户端
> 为保障项目安全，请不要随意在各个社交平台广泛传播该项目，包括不限于Bilibili、QQ、X（Twitter）、Discord
>
> 个人兴趣而制作，开发目的在于学习和探索，一切开发皆在学习，请勿用于非法用途
>
> 因使用本项目产生的一切问题与后果由使用者自行承担，项目开发者不承担任何责任
>
> 因项目特殊性，随时会删档

### 运行环境
* Java 21 及以上
* x86_64 或 ARMv8
* glibc (linux only)
* 内存 ≥ 200M

### 使用
```bash
java -jar client.jar -u <用户名/手机号> -p <密码>
````

### OpenWrt 部署
目前仅支持 x86_64 及 ARMv8 架构运行。

默认 OpenWRT 环境为 musl 运行时，请使用安装 Docker 软件包部署。当以 Docker 运行时，请包含 `--network host` 参数

推荐容器：openjdk:21

![](imgs/01.png)
![](imgs/02.png)

```bash
docker build -t dialer .
docker run -itd -e DIALER_USER=<用户名/手机号> -e DIALER_PASSWORD=<密码> --name dialer-client --network host --restart=always dialer
```

Dockerfile
```dockerfile
FROM openjdk:21
WORKDIR /app
COPY run.sh /app
COPY client.jar /app
CMD ["./run.sh"]
```
run.sh
```bash
#!/bin/sh
java -jar client.jar -u ${DIALER_USER} -p ${DIALER_PASSWORD} -d
```


### 构建
需要 Java 版本 >= 20
```bash
./gradlew jar
```
