# openwrt-gitpod
## 云编译openwrt

[lede源码地址](https://github.com/coolsnowwolf/lede)

### **第一次编译的命令行：**
1. 配置基础环境
1.1 
```bash
sudo apt-get update
```
1.2. 
```bash
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync
```

2. 拉取 lede 大源码
```bash
git clone https://github.com/coolsnowwolf/lede
````

3. 进入 lede 目录
```bash
cd lede
```

4. 更新并安装所有 feeds 
4.1 
```bash
./scripts/feeds update -a
```
4.2 
```bash
./scripts/feeds install -a
```

5. 测试编译 生成配置文件 `.config`
```bash
make menuconfig
```

6. 下载 dl 库
```bash
make -j8 download V=s
```

7. 开始编译工作
```bash
make -j1 V=s
```

### **第二次编译的命令行：**

1. 进入工作目录
```bash
cd lede
```
2. 更新源码
```bash
git pull
```
3. 更新安装 feeds
```bash
./scripts/feeds update -a && ./scripts/feeds install -a
```
4. 测试编译
```bahs
make defconfig
```
5. 下载 dl 库
```bash
make -j8 download
```
6. 编译（可以根据电脑核心来定 j 后面的数字）
```bash
make -j$(($(nproc) + 1)) V=s
```


如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
```
```bash
make menuconfig
```
```bash
make -j$(($(nproc) + 1)) V=s
```

### 编译完成后输出路径：bin/targets

## Git 提交

```bash
git add .
```
demo 为说明
```bash
git commit  -m "demo"
```
master 是分支名称
```bash
git push -u origin master
```
```bash
src-git kenzo https://github.com/kenzok8/openwrt-packages
```
```bash
src-git small https://github.com/kenzok8/small
```