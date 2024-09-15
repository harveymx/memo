## IPAD上部署Stable Diffusion
研究AI绘图，将Ipad Pro上的M1芯片利用起来，比较surfaceLaptop4的11代i7+xe集显
### Road1：适用ISH的Alpine Linux系统部署 - todo...还没有验证通过，因为这个模拟的apline linux是x86的
* AppStore下载iISH，内置Alpine Linux，很是精简
* 配置ISH，调整appearance、icon等,让它更顺眼一些
* 内置APK安装的源的python(3.9)版本旧，(来自知乎@Geometryolife)换USTC源：
  vi /etc/apk/repositories
  # 阿里云源
  https://mirrors.aliyun.com/alpine/v3.20/main
  https://mirrors.aliyun.com/alpine/v3.20/community
  # 中科大源
  https://mirrors.ustc.edu.cn/alpine/v3.20/main
  https://mirrors.ustc.edu.cn/alpine/v3.20/community
  -[问题]-在重启后失效，写个脚本，开机后执行
  vi /root/repo.sh
  #!/bin/ash
  echo "https://mirrors.aliyun.com/alpine/v3.20/main" > /etc/apk/repositories
  echo "https://mirrors.aliyun.com/alpine/v3.20/community" >> /etc/apk/repositories
  echo "https://mirrors.ustc.edu.cn/alpine/v3.20/main" >> /etc/apk/repositories
  echo "https://mirrors.ustc.edu.cn/alpine/v3.20/community" >> /etc/apk/repositories
  
  注：如果外网速度好，推荐用官方源：
  echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
  echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

  在/etc/profile文件里加入一条语句，让iSH在启动时加载脚本：
  vi /etc/profile
  source /root/repo.sh

* 安装软件
  apk update
  apk upgrade --available
  //apk add fish （验证: fish --version）
  apk add python3 py-pip (验证：py3 --version, pip --version)
  apk add git
  todo...................................

### Road2：使用liuliu的IPAD APP：DrawthingsAI
主要是苹果为了专属芯片，开发一个适用于mac系统的SD系统，并在github上开源。不少优秀的开发者利用这个开源基础框架，开发了可以在mac和ipad、甚至iphone上纯本地运营的AI生图APP，其中DrawthingsAI是针对ipad的APP，更新很快。已经在APPStore下载安装，正在研究使用它。
 
 update road2@2024-09-15