# My Linux Setup

## 使用WSL2安装Ubuntu 24.04 LTS

~~因为安装Ubuntu比较早，未记录安装过程日志，就在后文放几个报错信息及我的解决过程吧~~

## 报错记录及其解决

### Qemu 模拟器安装

在Qemu 模拟器安装时，运行：
```
./configure --target-list=riscv64-softmmu,riscv64-linux-user
```
报错信息如下:
```
Using './build' as the directory for build output
ERROR: Cannot find Ninja
```
查阅资料可知Qemu必需的ninja构建系统未安装，解决方法为安装Ninja即可。

### 安装并配置好zsh后无法使用原指令

在已安装cargo的zsh环境下，运行

```
cargo --version
```
提示：
```
zsh: correct 'cargo' to '.cargo' [nyae]?
```
查阅资料，解决方法：

打开```.zshrc```:

```
open ~/.zshrc
```
在```# User configuration```之后添加：
```
source ~/.bash_profile
```
然后退出zsh，重新打开zsh，再次运行```cargo --version```:
```
warning: `/home/wxh1104/.cargo/config` is deprecated in favor of `config.toml`
note: if you need to support cargo 1.38 or earlier, you can symlink `config` to `config.toml`
warning: `/home/wxh1104/.cargo/config` is deprecated in favor of `config.toml`
note: if you need to support cargo 1.38 or earlier, you can symlink `config` to `config.toml`
cargo 1.82.0 (8f40fc59f 2024-08-21)
```
再次查阅资料，Cargo 还支持没有 .toml 后缀的 .cargo/config 文件。对于 .toml 的支持是从 Rust 1.39 版本开始，同时也是目前最推荐的方式。

查看```.cargo```文件夹，发现有三个文件：
```
bin  config  env
```
解决方法：
```.cargo```文件夹下执行：
```
ln -s ./config ./config.toml 
```