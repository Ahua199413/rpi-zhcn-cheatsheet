树莓派中文参考卡片
==================================================

系统安装
------------------------------

### sudo raspi-config

* 1 Expand Filesystem 分区扩展
* 2 Change User Password 更改pi口令(推荐更改)
* 3 Enable Boot to Desktop 启动选项
 * * Console 文字终端(默认)
 * * Desktop 图形环境+LXDE桌面
 * * Scratch 小猫编程(图形环境无桌面)
* 4 I18n options 国际化选项  
  如果界面不能显示中文，则执行`LANG=C`临时改系统语言为英语，再重进`raspi-config`。
 * * I1 Locale 语言支持
  * * * 操作键: `PgUp`, `PgDn`, `Space`, `Tab`, `Enter`, `方向`
  * * * 必要：`en_US.UTF-8`
  * * * 必要：`zh_CN.UTF-8`
  * * * 可选：`zh_CN.GB18030`
 * * I2 Timezone 时区 `Asia/Shanghai`
 * * I3 Keyboard 键盘布局
  * * * 硬件类型：Generic 104-key PC
  * * * 键盘布局：Other
  * * * 国家地区：Chinese
  * * * 键盘布局：Chinese
  * * * 变换键：No AltGr Key
  * * * 多功能键：No compose key
  * * * Ctrl+Alt+Bksp：Yes
* 8 Advanced Options 高级选项
 * * A2 Hostname 主机名(可选更改)

### APT 软件管理器

#### 软件源镜像站

镜像站列表：

* 树莓爱好者整理汇总（推荐）  
  <http://t.cn/8k4MkIx>  
  <http://www.shumeipai.org/system-mirrors>
* Raspbian 官方网站  
  <http://t.cn/zj8aFYM>  
  <http://www.raspbian.org/RaspbianMirrors>  

更换软件源 `sudo nano /etc/apt/sources.list`  

`sources.list`内容：

    deb <url> wheezy main contrib non-free rpi
    deb-src <url> wheezy main contrib non-free rpi

#### 系统升级

* 更新软件列表 `sudo apt-get update`  
  （安装新软件如有任何错误，就先update）
* 升级所有软件 `sudo apt-get upgrade`

#### 软件包管理

* 安装 `sudo apt-get install <name>`
* 卸载 `sudo apt-get remove <name>`（只删程序）
* 卸载 `sudo apt-get purge <name>`（也删配置文件）
* 搜索 `apt-cache search <keyword>`

底层硬件
------------------------------

### GPIO

#### P1 GPIO双排针

奇数排：

* P1-02 5V0 靠近板角
* P1-04 5V0
* P1-06 GND
* P1-08 GPIO14 TXD
* P1-10 GPIO15 RXD
* P1-12 GPIO18
* P1-14 GND
* P1-16 GPIO23
* P1-18 GPIO24
* P1-20 GND
* P1-22 GPIO25
* P1-24 GPIO8 SPI0:/CE0
* P1-26 GPIO7 SPI0:/CE1

奇数排：

* P1-01 3V3 方块焊点
* P1-03 GPIO2 I2C1:SDA 1K8上拉
* P1-05 GPIO3 I2C1:SCL 1K8上拉
* P1-07 GPIO4
* P1-09 GND
* P1-11 GPIO17
* P1-13 GPIO27
* P1-15 GPIO22
* P1-17 3V3
* P1-19 GPIO10 SPI0:MOSI 	
* P1-21 GPIO9 SPI0:MISO 	
* P1-23 GPIO11 SPI0:SCLK 	
* P1-25 GND

5V0在保险之后，所有3V3总和最大输出能力50mA

对于Rev1: I2C1->I2C0, GPIO:2->0, 3->1, 27->21

#### P5 Rev2附加GPIO

奇数排：

* P5-01	5V0 靠近板角,方焊点
* P5-03 GPIO28 I2C0:SDA
* P5-05	GPIO30 
* P5-07 GND

偶数排：

* P5-02 3V3
* P5-04 GPIO29 I2C0:SCL
* P5-06 GPIO31
* P5-08 GND

Rev2另加P6接口，用镊子短路可让树莓派硬重启。

版本管理系统
------------------------------

### Git

最新Raspbian附带。其他系统：安装`git`或`git-core`。

建立仓库

* 空仓库 `git init`
* 克隆远程 `git clone <url>`

基本概念

* 项目主线，默认本地分支 `master`
* 默认远程分支 `origin`
* 当前分支 `HEAD`

文件操作

* 查看状态 `git status`
* 加入文件 `git add <filename>`
* 加入所有 `git add .`
* 删除文件 `git rm <filename>`
* 文件移动 `git mv <src> <dest>`

提交操作

* 更新本地副本 `git pull`
* 提交本地修改 `git commit`
* 快速提交(承认所有文件更改) `git commit -a`
* 推送远程仓库 `git push`

分支操作

* 列出分支 `git branch`
* 复制分支 `git branch <new-branch>`  
* 删除分支 `git branch -d <branch>`
* 切换分支 `git checkout <branch>`
* 并入分支 `git merge <branch>`  
* 标注标签 `git tag <v1.0>`
* 推送分支到远程 `git push origin <branch>`
* 删除远程分支 `git push origin :<branch>`

修正错误

* 查看提交历史 `git log`
* 本次提交算作上次提交 `git commit --amend`  
  (修正上次提交的错误)
* 丢弃所有未提交改动 `git reset --hard HEAD`
* 回滚到某个提交 `git revert <commit-hash>`


