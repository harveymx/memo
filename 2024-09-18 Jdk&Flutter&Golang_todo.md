## 2024-09-17 JDK、Flutter、Golang
* 安装JDK
sudo apt install openjdk-17-jdk gradle
vi ~/.config/fish/config.fish
在文件中加入：export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-jdk

* 安装android commmand line tools
//来自https://segmentfault.com/a/1190000044077220 :
curl https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -o /tmp/cmd-tools.zip
mkdir -p android/cmdline-tools
unzip -q -d android/cmdline-tools /tmp/cmd-tools.zip
mv android/cmdline-tools/cmdline-tools android/cmdline-tools/latest
rm /tmp/cmd-tools.zip # delete the zip file (optional)

设置环境变量（vi ~/.config/fish/config.fish）:
export ANDROID_HOME="$HOME/android"
export ANDROID_SDK_ROOT="$ANDROID_HOME"
export PATH="$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$PATH"

命令行同意android licenses:
yes | sdkmanager --licenses

* 安装Flutter
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
git clone -b dev https://github.com/flutter/flutter.git
设置环境变量（vi ~/.config/fish/config.fish）:
export PATH="$HOME/flutter/bin:$PATH"
运行命令，检查验证：
flutter doctor

* 安装Golang
//来自 https://dev.to/deadwin19/how-to-install-golang-on-wslwsl2-2880 ：
wget https://dl.google.com/go/go1.23.1.linux-amd64.tar.gz
sudo tar -xvf go1.23.1.linux-amd64.tar.gz
sudo mv go /usr/local

设置环境变量（vi ~/.config/fish/config.fish）:
export GOROOT="/usr/local/go"
export GOPATH="$HOME/go"
export PATH="$GOPATH/bin:$GOROOT/bin:$PATH"
运行命令，检查验证：
go version

rm go1.23.1.linux-amd64.tar.gz

* (安装FIClash)-> 改安装SheelCrsh，整合度更高，不需要上述依赖安装
https://github.com/juewuy/ShellCrash/
其他知识：https://www.joeyne.cool/http/proxy/ubuntu-%e5%ae%89%e8%a3%85clash%e5%b9%b6%e9%85%8d%e7%bd%ae%e5%bc%80%e6%9c%ba%e5%90%af%e5%8a%a8/