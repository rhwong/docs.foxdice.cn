> 本站采用 [免费许可](https://github.com/ZeroDream-CN/SakuraPanel/blob/master/LICENSE)，不用于出租盈利，且同时限制**用户**仅可用于个人非盈利使用。
## 简介

[大狐狐 Frp](https://sakura.zerda.top/) 是由 [贰狐](https://www.aobacore.com/) 使用 [SakuraPanel](https://github.com/ZeroDream-CN/SakuraPanel) 面板搭建的免费内网穿透服务，旨在方便大家游戏联机

使用的服务器并非高并发高负载的专用服务器，仅仅是我目前闲置中相对带宽较高的服务器

~~有高带宽服务器，但是由于流量费用过高暂时不考虑惹，等一个赞助商~~

## 注册账户

?> [点此跳转注册页面](https://sakura.zerda.top/?page=register)

按照注册页面要求如实填写注册信息，尽量使用QQ邮箱

!> 请注意，邀请码的发送是自动流程，请确保发送的消息不包含多余的文字

邀请码的获取：请先添加贰狐的QQ，然后在私聊中发送 `申请邀请码`

## 创建隧道

以联机 `东方异文石 - 爱亚利亚黎明：再造` 为例

?> `东方异文石 - 爱亚利亚黎明：再造` 采用 `TCP` 协议通过 `6510` 端口连接

首先，你需要创建一个隧道以供使用

点击左侧 **创建隧道** 选项卡，在页面中选择**地理位置较近**的服务器节点，这是为了降低延迟，提高游戏质量

然后点击 **随机端口** 按钮，或在**远程端口**输入框中手动键入一个30000-65535之间的值

**隧道类型**和**本地端口**已为你自动键入，若联机`东方异文石`则无需修改(其他游戏请按需修改隧道类型和本地端口)

!> `127.0.0.1` 是回送地址，在所有网络设备上，都指程序运行的当前本机

![bigfox_frp_01](_static\bigfox_frp_01.png ':size=80%')

然后直接忽略 ***高级设置** ，直接向下滚动，点击 **完成创建**

> 高级设置为选填，仅限有需求的用户使用，一般留空即可

## 软件下载

点击左侧的 [软件下载](https://sakura.zerda.top/?page=panel&module=download) 选项卡，跳转到下载页面

在本页面中按照系统版本下载你需要的软件

!> Windows 通常下载第一个`Windows i386`即可

软件下载好后是以压缩包的形式存在，请 **解压缩** 到一个位置

然后点此下载客户端启动脚本 [Windows](https://sakura.zerda.top/doc/startfrpc.cmd) |  [Linux](https://sakura.zerda.top/doc/startfrpc.sh)

将启动脚本放在刚才软件解压缩的位置，和 `frpc.exe` 同级，如图所示

![bigfox_frp_05](_static\bigfox_frp_05.png)

> 此软件为开源项目[FRP](https://github.com/fatedier/frp/)，下载链接为[官方发布](https://github.com/fatedier/frp/releases)，杀软误报请自行判断

## 常规设置

点击左侧 **配置文件** 选项卡

在上方选择刚才创建好隧道的服务器，然后将下方的配置文件内容**完全复制**

![bigfox_frp_02](_static\bigfox_frp_02.png)

然后打开刚才解压好的文件夹，找到 `frpc.ini`

![bigfox_frp_03](_static\bigfox_frp_03.png)

双击打开，删除里面原有的内容，将复制的配置文件内容 **覆盖粘贴** 进去，**保存**并退出

![bigfox_frp_04](_static\bigfox_frp_04.png)

## 启动程序

双击刚才下载好的启动脚本 `startfrpc.cmd` 即可运行

正常情况如图所示，显示 `start proxy success` 就是成功穿透

![bigfox_frp_06](_static\bigfox_frp_06.png)

此时你应该保持此程序最小化运行，**不可以关闭**(会立即断开连接)

此程序控制台页面包含你的密钥和隧道信息，**请不要随意截图给其他人！**

!> 若程序闪退，请检查配置文件或在网站检查账户状态

## 加入房间

!> 只有主机需要运行Frp程序，直接玩家直接联机即可

远程服务器的IP和所穿透的端口号在配置文件中即可查看

![bigfox_frp_07](_static\bigfox_frp_07.png)

其他玩家在游戏内输入此IP和端口号即可加入游戏

![bigfox_frp_08](_static\bigfox_frp_08.png)

## 示例：单节点多隧道分别运行

假如你在一个节点上创建了两个隧道，如以下代码所示，你的配置文件中会出现三个配置节

``` ini
[common]
server_addr = 49.232.207.98
server_port = 2333
tcp_mux = true
protocol = tcp
user = 7433a33348a70139
token = BigFoxFrpToken
dns_server = 114.114.114.114
 
[5C62K9S3VD]
privilege_mode = true
type = tcp
local_ip = 127.0.0.1
local_port = 6510
remote_port = 65100
use_encryption = false
use_compression = false
 
[90TLL9QJG7]
privilege_mode = true
type = tcp
local_ip = 127.0.0.1
local_port = 6510
remote_port = 40808
use_encryption = false
use_compression = false
```

配置节之间以**空白行**进行了分割，最上方的 `[common]` 配置节为认证信息配置节，此配置节不可删除

例如你需要**单独使用** `[90TLL9QJG7]` 这个隧道，那么你的配置文件就是

``` ini
[common]
server_addr = 49.232.207.98
server_port = 2333
tcp_mux = true
protocol = tcp
user = 7433a33348a70139
token = BigFoxFrpToken
dns_server = 114.114.114.114
 
[90TLL9QJG7]
privilege_mode = true
type = tcp
local_ip = 127.0.0.1
local_port = 6510
remote_port = 40808
use_encryption = false
use_compression = false
```

## 示例：单端口多节点同时运行

联机的时候，大家地理位置天南地北，有时候某个人网络不佳可能会比较尴尬

假设A在北京、B在内蒙古、C在香港、D在东京

A开设主机，穿透至北京服务器节点供大家联机

那么A与B的实际延迟可能在50ms左右、A与C的实际延迟可能在100ms左右、A与D的实际延迟可能在200ms左右

且由于出国线路问题，C和D很有可能会经常掉线

那么此时我们可以**再创建一个香港隧道**，**复制**一份frp程序文件夹，并**修改配置文件**为香港节点，然后**同时开启**两个frp程序

这样就可以让B连接北京服务器IP，而C与D连接香港服务器IP，以提高网络质量稳定性