# 方舟开服要什么配置、花多少钱：4核8G 够几个人？端口为什么总连不上？从选机器到开服一次讲清（附云服务器套餐对比）

开一个《方舟：生存进化》的服，机器不用买多贵。2 到 4 个人玩，4 核 8G 起步；6 人以上，或者要跑 Ragnarok、Valguero 这类大地图，内存加到 16G。按第三方开服教程统计的云服务器行情，月成本大致落在几十元到几百元这个区间，具体看你租哪一档。

真正让人卡住的通常不是钱，是端口。方舟服务端全部走 UDP，7777 和 7778 必须一起映射出去，只开 7777 的服务器，朋友能搜到、能点进去，然后卡在加载界面不动。这个坑每年都有新服主踩。

下面把三件事讲清楚：你的服到底要多大机器、端口怎么规划、命令怎么敲。最后给一份按人数和预算选档位的规则。

> **选购速览**：绝大多数人从 4 核 8G 这一档开始就够，2 到 4 人小队甚至 4 核 4G 也能跑单图。要跑多地图或装大型 MOD，直接上 8 核 16G，别在中间档反复升级。雨云当前在售的档位和实时报价在这里，价格以页面显示为准：👉 [查看雨云云服务器套餐与报价](https://bit.ly/RaiNyun)

## 雨云当前在售的通用云服务器档位

先说明一点：雨云官网的实时价格会随机房和活动调整，下表是按公开整理资料汇总的国内机房通用云服务器档位，用来判断"我该买多大"，下单前请以官网页面为准。

| 档位 | CPU / 内存 / 硬盘 | 带宽（上行/下行） | 月付参考价 | 适合谁 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 入门版 | 1 核 / 1G / 30G | 10M / 20M | ¥18 | 只跑单图、2 人以内，内存吃紧 | [查看该档位](https://bit.ly/RaiNyun) |
| 标准版 | 2 核 / 2G / 30G | 15M / 50M | ¥25 | 不推荐开方舟，内存不够 | [查看该档位](https://bit.ly/RaiNyun) |
| 中配版 | 2 核 / 4G / 30G | 20M / 50M | ¥35 | 单图极限起步，加载慢、易卡 | [查看该档位](https://bit.ly/RaiNyun) |
| 进阶版 | 4 核 / 4G / 30G | 25M / 100M | ¥48 | 2 到 3 人纯净服，单张地图 | [查看该档位](https://bit.ly/RaiNyun) |
| 高级版 | 4 核 / 8G / 30G | 35M / 150M | ¥88 | **最常被选的方舟档位**，2 到 6 人带 MOD | [查看该档位](https://bit.ly/RaiNyun) |
| 旗舰版 | 8 核 / 16G / 30G | 35M / 150M | ¥158 | 6 人以上、大地图、多图集群 | [查看该档位](https://bit.ly/RaiNyun) |

雨云还有香港、美国机房，以及标注了具体 CPU 型号的高频机型产品线（如 Ryzen、i9 系列），配置和价格与上表不同。开方舟这类对单核性能敏感的服，高频机型是值得多花的那部分钱，后面会解释为什么。

硬盘这一列要单独提醒：上表是 30G 系统盘，方舟纯净服务端本体按不同教程的说法在 15G 到 60G 之间（差异主要在是否含全部 DLC 地图），装几个大 MOD 就奔着 25G 以上去了。买之前把磁盘算够，或者确认能单独加挂数据盘。

## 你的服到底要多大：三种口径，按最严的那个算

网上关于"方舟要多少配置"的说法有分歧，因为它本来就取决于三件不同的事：人数、地图数量、单核性能。

**按人数估**（第三方教程的统计口径）：1 到 5 人用 2 核 4 到 8G，5 到 15 人用 4 核 8 到 16G，15 到 30 人用 4 到 8 核 16 到 32G，30 人以上要 8 核加 32G 起。

**按地图估**：单张地图 4G 能跑起来，但那是靠内存压缩硬撑，会有性能损失、容易卡顿；6G 以上才算稳。地图是叠加的，一张图一份内存，所谓"11 通"（11 张地图互联）至少需要 64G 内存。核心数可以按"一核一图"粗算。

**按单核性能估**：方舟服务端的主线程是单核的。单张地图 4 个较强的 vCPU 就能起步，中型公开服评估到 6 到 8 个较强 vCPU。关键线程吃满之后，继续堆同档核心基本没有改善。

三种口径合起来，结论是这样：

- 2 到 4 人、单张地图、不装大 MOD：**4 核 4G 到 4 核 8G**，磁盘留 30G 以上
- 4 到 8 人、单图带几个 MOD：**4 核 8G**，内存不要再低
- 6 人以上或大地图（Ragnarok、Fjordur）：**4 核 16G 起**
- 多地图互联：按每图 6G 往上加，别按 4G 算

有一个选购细节比核数重要得多：**看清楚套餐标的 CPU 型号和主频**。方舟是单核性能敏感型应用，一颗高主频的 4 核通常比低主频的 8 核表现更好。国内不少便宜机型用的是至强 E5 老架构，核心多、单核弱，PVP 服尤其吃亏，国外开方舟服普遍用 3.5GHz 以上的处理器。另外不要买"突发性能实例"（t 系列那类），CPU 积分耗尽后会降频，表现为全服突然一起卡。

至于带宽，方舟要求真不高。10 人左右的服上行 5Mbps 通常够用，数据传输集中在玩家连接和区域加载的瞬间，平时流量很小。

## 端口这一步错了，前面全白搭

方舟服务端用到的端口：

| 端口 | 协议 | 用途 |
| --- | --- | --- |
| 7777 | UDP | 游戏主端口，必须 |
| 7778 | UDP | 配套通道，必须，只开 7777 会卡加载 |
| 27015 | UDP | Steam 查询端口，服务器列表可见 |
| 32330 | UDP | RCON 管理端口，可选 |

**全部是 UDP。** 映射时选成 TCP，客户端一定连不上。

27015 这个端口存在两种说法。一部分教程写它是 TCP（Steam 查询），另一部分写它是 UDP 且必须。较新的开服教程把它列在 UDP 里，同时说明方舟全部走 UDP。实操建议是**按 UDP 放行，如果服务器列表刷不出来，再把 TCP 一起放开**，两个协议都放行不会有害。这是操作建议，不是官方口径。

NAT 型服务器能不能开方舟？能，而且价格比独立 IP 便宜一半以上，适合长期开服。映射写法举例：


UDP 外部 17777 → 内部 7777
UDP 外部 17778 → 内部 7778
UDP 外部 17015 → 内部 27015


**映射出来的外部端口是几，客户端就连几。** 启动参数里的 `QueryPort` 必须和实际映射出去的那个外部端口一致，否则服务器列表刷不出来，玩家只能靠直连。

客户端进服有两条路：游戏内勾选"显示非官方服务器"搜服务器名，或者用 Steam 的服务器收藏夹直连 `IP:端口`。社区列表刷新本来就慢，直连最稳。NAT 用户填映射后的外部端口。

如果你打算用 NAT 型，买之前先确认一件事：控制台里能不能自己添加 UDP 端口映射规则，能不能一次加三条。面板型产品的端口映射权限差别很大，有的只给固定几个端口。这一点直接问客服最快。👉 [进雨云控制台或咨询客服确认端口映射能力](https://bit.ly/RaiNyun)

## 从零开服：四条命令加一个启动脚本

方舟服务端原生支持 Linux，不需要 Wine。系统选 Ubuntu 22.04 或 Debian 12。

**第一步，装依赖和 SteamCMD。**

bash
sudo apt update
sudo apt install -y lib32gcc-s1 curl wget tar screen libssl-dev libcurl4-openssl-dev

mkdir ~/steamcmd && cd ~/steamcmd
wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
tar xzf steamcmd_linux.tar.gz


**第二步，下载服务端。App ID 是 376030，首次安装必须带 `validate`。**

bash
./steamcmd.sh +force_install_dir ~/ark +login anonymous +app_update 376030 validate +quit


后续更新可以去掉 `validate` 加快速度，但游戏大版本更新后进不去的时候，带上它重新跑一遍通常能修好。

**第三步，写启动脚本。** 参数一个都不能少写：

bash
#!/bin/bash
cd ~/ark/ShooterGame/Binaries/Linux
./ShooterGameServer "TheIsland?listen?SessionName=我的方舟服?ServerPassword=123456?ServerAdminPassword=admin666?Port=7777?QueryPort=27015?RCONPort=32330?MaxPlayers=20" -server -log


- `TheIsland` 是地图名，可换成 Ragnarok、TheCenter、Aberration、Extinction、Valguero、Fjordur
- `?listen` 必须有，缺了客户端连不上
- `ServerAdminPassword` 务必改掉，这是游戏内 `enablecheats` 用的密码
- `Port` 和 `QueryPort` 要和你的端口映射对得上

**第四步，挂后台。** 临时用 screen：

bash
screen -S ark
~/ark/start-ark.sh
# Ctrl+A 然后按 D 脱离，服务器继续跑
# screen -r ark 回到控制台


长期开服建议做成 systemd 服务，崩了自动拉起、开机自启：

ini
[Unit]
Description=ARK Server
After=network.target

[Service]
Type=simple
WorkingDirectory=/root/ark
ExecStart=/root/ark/start-ark.sh
Restart=on-failure
RestartSec=30
LimitNOFILE=100000

[Install]
WantedBy=multi-user.target


bash
sudo systemctl daemon-reload
sudo systemctl enable ark && sudo systemctl start ark


首次加载地图要 3 到 5 分钟，属于正常。一直卡在初始化多半是内存不够，可以先加 swap 顶一下：

bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile && sudo swapon /swapfile


swap 只是应急，长期靠它跑方舟会明显掉性能，该升内存还是得升。

## 开起来之后：倍率、MOD、卡顿和备份

**难度和倍率**写在 `GameUserSettings.ini` 的 `[ServerSettings]` 和 `Game.ini` 里。最关键的参数是 `OverrideOfficialDifficulty=5.0`，配合 `DifficultyOffset=1.0`，公式是难度乘 30 等于野生恐龙最大等级，5.0 就是 150 级，驯服后可训到 225 级左右。小团体私服常把 `TamingSpeedMultiplier` 和 `HarvestAmountMultiplier` 调到 5 到 10，接近官服的硬核服保持 1 到 2。

`bAllowFlyerSpeedLeveling=False` 建议保持默认，这是官方的平衡设置，放开飞行生物加速度之后 PVP 会失衡。

**MOD** 装在 `ActiveMods=` 里，逗号分隔。MOD ID 就是创意工坊链接 `?id=` 后面那串数字，比如 Structures Plus 是 `731604991`。服务端启动时会自动下载。两件事要知道：MOD 按列表顺序加载，后加载的会覆盖先加载的内容；MOD 更新可能导致存档不兼容，**更新前先备份**。

装 MOD 会让内存和磁盘同时往上涨，这也是前面建议磁盘留足的原因。

**周期性卡顿几秒**多半是自动保存。默认 15 分钟一次，改成 `AutoSavePeriodMinutes=30` 能缓解。**运行几天越来越卡、重启就恢复**，是内存泄漏，最有效的办法是每天凌晨定时重启一次，用 crontab 挂个任务就行。

**备份**只需盯住一个目录：`~/ark/ShooterGame/Saved/SavedArks`，里面的 `.ark` 是世界存档、`.arktribe` 是部落、`.arkprofile` 是玩家数据。

bash
tar czf ~/ark_backup_$(date +%m%d).tar.gz -C ~/ark/ShooterGame Saved


出事了先别慌，服务端每次自动保存会留一份 `地图名.ark.bak`，把 `.bak` 改回 `.ark` 有机会救回来（改之前先把损坏的文件另存一份）。

## 这三种情况，别租云服务器

**单人玩或者只想局域网联机。** 游戏自带的非专用主机模式就够，虽然有人数上限和距离限制，但不花钱、不用配端口。

**家里有闲置的高配 NAS 或旧电脑。** 群晖 DS220+ 这类设备有人实测过：单张地图需要 4G 内存，原装 4G 明显不够，得升到 16G；虚拟机分配 10G 内存、2 个虚拟核心（占用率通常低于 30%）、初始 200G 存储（4 个官方地图就占满）。虚拟机磁盘选"厚置备延迟置零"，启用 Intel VT-x，网络适配器选桥接。缺点是家庭宽带没有防御、线路共享，被干扰时延迟和卡顿比云服务器明显。

**你玩的其实是手游私服。** 《方舟》手游进私服是另一套流程：需要 Google Play 环境、谷歌账号，在 UNOFFICIAL SERVERS 列表里选服输密码。跟本文的 PC 服务端搭建没有关系。顺带说一句，搜"方舟开服"时还会撞到《明日方舟》的更新公告，那也不是一回事。

## 最后：按你的情况选哪一档

- **2 到 3 人、单图、纯净服**：4 核 4G，磁盘给到 30G 以上，月付几十元这一档
- **4 到 6 人、带几个 MOD**：4 核 8G，这是方舟最常见的选择
- **6 人以上或大地图**：8 核 16G，别在 4 核 16G 上纠结太久
- **多地图互联**：按每图 6G 累加，直接跳到高内存档位

下单前确认两件事：**一是你的机型能不能自己加 UDP 端口映射**（NAT 型必须能加 7777、7778、27015 三条）；**二是磁盘给 30G 够不够**，取决于你装不装 MOD、开几张图，拿不准就往大了留。

雨云的新用户注册后绑定微信通常能领到首月折扣券，具体力度和有效期以官网活动页为准：👉 [从雨云挑一台合适的机器开始搭服](https://bit.ly/RaiNyun)
# 方舟开服要什么配置、花多少钱：4核8G 够几个人？端口为什么总连不上？从选机器到开服一次讲清（附云服务器套餐对比）

开一个《方舟：生存进化》的服，机器不用买多贵。2 到 4 个人玩，4 核 8G 起步；6 人以上，或者要跑 Ragnarok、Valguero 这类大地图，内存加到 16G。按第三方开服教程统计的云服务器行情，月成本大致落在几十元到几百元这个区间，具体看你租哪一档。

真正让人卡住的通常不是钱，是端口。方舟服务端全部走 UDP，7777 和 7778 必须一起映射出去，只开 7777 的服务器，朋友能搜到、能点进去，然后卡在加载界面不动。这个坑每年都有新服主踩。

下面把三件事讲清楚：你的服到底要多大机器、端口怎么规划、命令怎么敲。最后给一份按人数和预算选档位的规则。

> **选购速览**：绝大多数人从 4 核 8G 这一档开始就够，2 到 4 人小队甚至 4 核 4G 也能跑单图。要跑多地图或装大型 MOD，直接上 8 核 16G，别在中间档反复升级。雨云当前在售的档位和实时报价在这里，价格以页面显示为准：👉 [查看雨云云服务器套餐与报价](https://bit.ly/RaiNyun)

## 雨云当前在售的通用云服务器档位

先说明一点：雨云官网的实时价格会随机房和活动调整，下表是按公开整理资料汇总的国内机房通用云服务器档位，用来判断"我该买多大"，下单前请以官网页面为准。

| 档位 | CPU / 内存 / 硬盘 | 带宽（上行/下行） | 月付参考价 | 适合谁 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 入门版 | 1 核 / 1G / 30G | 10M / 20M | ¥18 | 只跑单图、2 人以内，内存吃紧 | [查看该档位](https://bit.ly/RaiNyun) |
| 标准版 | 2 核 / 2G / 30G | 15M / 50M | ¥25 | 不推荐开方舟，内存不够 | [查看该档位](https://bit.ly/RaiNyun) |
| 中配版 | 2 核 / 4G / 30G | 20M / 50M | ¥35 | 单图极限起步，加载慢、易卡 | [查看该档位](https://bit.ly/RaiNyun) |
| 进阶版 | 4 核 / 4G / 30G | 25M / 100M | ¥48 | 2 到 3 人纯净服，单张地图 | [查看该档位](https://bit.ly/RaiNyun) |
| 高级版 | 4 核 / 8G / 30G | 35M / 150M | ¥88 | **最常被选的方舟档位**，2 到 6 人带 MOD | [查看该档位](https://bit.ly/RaiNyun) |
| 旗舰版 | 8 核 / 16G / 30G | 35M / 150M | ¥158 | 6 人以上、大地图、多图集群 | [查看该档位](https://bit.ly/RaiNyun) |

雨云还有香港、美国机房，以及标注了具体 CPU 型号的高频机型产品线（如 Ryzen、i9 系列），配置和价格与上表不同。开方舟这类对单核性能敏感的服，高频机型是值得多花的那部分钱，后面会解释为什么。

硬盘这一列要单独提醒：上表是 30G 系统盘，方舟纯净服务端本体按不同教程的说法在 15G 到 60G 之间（差异主要在是否含全部 DLC 地图），装几个大 MOD 就奔着 25G 以上去了。买之前把磁盘算够，或者确认能单独加挂数据盘。

## 你的服到底要多大：三种口径，按最严的那个算

网上关于"方舟要多少配置"的说法有分歧，因为它本来就取决于三件不同的事：人数、地图数量、单核性能。

**按人数估**（第三方教程的统计口径）：1 到 5 人用 2 核 4 到 8G，5 到 15 人用 4 核 8 到 16G，15 到 30 人用 4 到 8 核 16 到 32G，30 人以上要 8 核加 32G 起。

**按地图估**：单张地图 4G 能跑起来，但那是靠内存压缩硬撑，会有性能损失、容易卡顿；6G 以上才算稳。地图是叠加的，一张图一份内存，所谓"11 通"（11 张地图互联）至少需要 64G 内存。核心数可以按"一核一图"粗算。

**按单核性能估**：方舟服务端的主线程是单核的。单张地图 4 个较强的 vCPU 就能起步，中型公开服评估到 6 到 8 个较强 vCPU。关键线程吃满之后，继续堆同档核心基本没有改善。

三种口径合起来，结论是这样：

- 2 到 4 人、单张地图、不装大 MOD：**4 核 4G 到 4 核 8G**，磁盘留 30G 以上
- 4 到 8 人、单图带几个 MOD：**4 核 8G**，内存不要再低
- 6 人以上或大地图（Ragnarok、Fjordur）：**4 核 16G 起**
- 多地图互联：按每图 6G 往上加，别按 4G 算

有一个选购细节比核数重要得多：**看清楚套餐标的 CPU 型号和主频**。方舟是单核性能敏感型应用，一颗高主频的 4 核通常比低主频的 8 核表现更好。国内不少便宜机型用的是至强 E5 老架构，核心多、单核弱，PVP 服尤其吃亏，国外开方舟服普遍用 3.5GHz 以上的处理器。另外不要买"突发性能实例"（t 系列那类），CPU 积分耗尽后会降频，表现为全服突然一起卡。

至于带宽，方舟要求真不高。10 人左右的服上行 5Mbps 通常够用，数据传输集中在玩家连接和区域加载的瞬间，平时流量很小。

## 端口这一步错了，前面全白搭

方舟服务端用到的端口：

| 端口 | 协议 | 用途 |
| --- | --- | --- |
| 7777 | UDP | 游戏主端口，必须 |
| 7778 | UDP | 配套通道，必须，只开 7777 会卡加载 |
| 27015 | UDP | Steam 查询端口，服务器列表可见 |
| 32330 | UDP | RCON 管理端口，可选 |

**全部是 UDP。** 映射时选成 TCP，客户端一定连不上。

27015 这个端口存在两种说法。一部分教程写它是 TCP（Steam 查询），另一部分写它是 UDP 且必须。较新的开服教程把它列在 UDP 里，同时说明方舟全部走 UDP。实操建议是**按 UDP 放行，如果服务器列表刷不出来，再把 TCP 一起放开**，两个协议都放行不会有害。这是操作建议，不是官方口径。

NAT 型服务器能不能开方舟？能，而且价格比独立 IP 便宜一半以上，适合长期开服。映射写法举例：


UDP 外部 17777 → 内部 7777
UDP 外部 17778 → 内部 7778
UDP 外部 17015 → 内部 27015


**映射出来的外部端口是几，客户端就连几。** 启动参数里的 `QueryPort` 必须和实际映射出去的那个外部端口一致，否则服务器列表刷不出来，玩家只能靠直连。

客户端进服有两条路：游戏内勾选"显示非官方服务器"搜服务器名，或者用 Steam 的服务器收藏夹直连 `IP:端口`。社区列表刷新本来就慢，直连最稳。NAT 用户填映射后的外部端口。

如果你打算用 NAT 型，买之前先确认一件事：控制台里能不能自己添加 UDP 端口映射规则，能不能一次加三条。面板型产品的端口映射权限差别很大，有的只给固定几个端口。这一点直接问客服最快。👉 [进雨云控制台或咨询客服确认端口映射能力](https://bit.ly/RaiNyun)

## 从零开服：四条命令加一个启动脚本

方舟服务端原生支持 Linux，不需要 Wine。系统选 Ubuntu 22.04 或 Debian 12。

**第一步，装依赖和 SteamCMD。**

bash
sudo apt update
sudo apt install -y lib32gcc-s1 curl wget tar screen libssl-dev libcurl4-openssl-dev

mkdir ~/steamcmd && cd ~/steamcmd
wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
tar xzf steamcmd_linux.tar.gz


**第二步，下载服务端。App ID 是 376030，首次安装必须带 `validate`。**

bash
./steamcmd.sh +force_install_dir ~/ark +login anonymous +app_update 376030 validate +quit


后续更新可以去掉 `validate` 加快速度，但游戏大版本更新后进不去的时候，带上它重新跑一遍通常能修好。

**第三步，写启动脚本。** 参数一个都不能少写：

bash
#!/bin/bash
cd ~/ark/ShooterGame/Binaries/Linux
./ShooterGameServer "TheIsland?listen?SessionName=我的方舟服?ServerPassword=123456?ServerAdminPassword=admin666?Port=7777?QueryPort=27015?RCONPort=32330?MaxPlayers=20" -server -log


- `TheIsland` 是地图名，可换成 Ragnarok、TheCenter、Aberration、Extinction、Valguero、Fjordur
- `?listen` 必须有，缺了客户端连不上
- `ServerAdminPassword` 务必改掉，这是游戏内 `enablecheats` 用的密码
- `Port` 和 `QueryPort` 要和你的端口映射对得上

**第四步，挂后台。** 临时用 screen：

bash
screen -S ark
~/ark/start-ark.sh
# Ctrl+A 然后按 D 脱离，服务器继续跑
# screen -r ark 回到控制台


长期开服建议做成 systemd 服务，崩了自动拉起、开机自启：

ini
[Unit]
Description=ARK Server
After=network.target

[Service]
Type=simple
WorkingDirectory=/root/ark
ExecStart=/root/ark/start-ark.sh
Restart=on-failure
RestartSec=30
LimitNOFILE=100000

[Install]
WantedBy=multi-user.target


bash
sudo systemctl daemon-reload
sudo systemctl enable ark && sudo systemctl start ark


首次加载地图要 3 到 5 分钟，属于正常。一直卡在初始化多半是内存不够，可以先加 swap 顶一下：

bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile && sudo swapon /swapfile


swap 只是应急，长期靠它跑方舟会明显掉性能，该升内存还是得升。

## 开起来之后：倍率、MOD、卡顿和备份

**难度和倍率**写在 `GameUserSettings.ini` 的 `[ServerSettings]` 和 `Game.ini` 里。最关键的参数是 `OverrideOfficialDifficulty=5.0`，配合 `DifficultyOffset=1.0`，公式是难度乘 30 等于野生恐龙最大等级，5.0 就是 150 级，驯服后可训到 225 级左右。小团体私服常把 `TamingSpeedMultiplier` 和 `HarvestAmountMultiplier` 调到 5 到 10，接近官服的硬核服保持 1 到 2。

`bAllowFlyerSpeedLeveling=False` 建议保持默认，这是官方的平衡设置，放开飞行生物加速度之后 PVP 会失衡。

**MOD** 装在 `ActiveMods=` 里，逗号分隔。MOD ID 就是创意工坊链接 `?id=` 后面那串数字，比如 Structures Plus 是 `731604991`。服务端启动时会自动下载。两件事要知道：MOD 按列表顺序加载，后加载的会覆盖先加载的内容；MOD 更新可能导致存档不兼容，**更新前先备份**。

装 MOD 会让内存和磁盘同时往上涨，这也是前面建议磁盘留足的原因。

**周期性卡顿几秒**多半是自动保存。默认 15 分钟一次，改成 `AutoSavePeriodMinutes=30` 能缓解。**运行几天越来越卡、重启就恢复**，是内存泄漏，最有效的办法是每天凌晨定时重启一次，用 crontab 挂个任务就行。

**备份**只需盯住一个目录：`~/ark/ShooterGame/Saved/SavedArks`，里面的 `.ark` 是世界存档、`.arktribe` 是部落、`.arkprofile` 是玩家数据。

bash
tar czf ~/ark_backup_$(date +%m%d).tar.gz -C ~/ark/ShooterGame Saved


出事了先别慌，服务端每次自动保存会留一份 `地图名.ark.bak`，把 `.bak` 改回 `.ark` 有机会救回来（改之前先把损坏的文件另存一份）。

## 这三种情况，别租云服务器

**单人玩或者只想局域网联机。** 游戏自带的非专用主机模式就够，虽然有人数上限和距离限制，但不花钱、不用配端口。

**家里有闲置的高配 NAS 或旧电脑。** 群晖 DS220+ 这类设备有人实测过：单张地图需要 4G 内存，原装 4G 明显不够，得升到 16G；虚拟机分配 10G 内存、2 个虚拟核心（占用率通常低于 30%）、初始 200G 存储（4 个官方地图就占满）。虚拟机磁盘选"厚置备延迟置零"，启用 Intel VT-x，网络适配器选桥接。缺点是家庭宽带没有防御、线路共享，被干扰时延迟和卡顿比云服务器明显。

**你玩的其实是手游私服。** 《方舟》手游进私服是另一套流程：需要 Google Play 环境、谷歌账号，在 UNOFFICIAL SERVERS 列表里选服输密码。跟本文的 PC 服务端搭建没有关系。顺带说一句，搜"方舟开服"时还会撞到《明日方舟》的更新公告，那也不是一回事。

## 最后：按你的情况选哪一档

- **2 到 3 人、单图、纯净服**：4 核 4G，磁盘给到 30G 以上，月付几十元这一档
- **4 到 6 人、带几个 MOD**：4 核 8G，这是方舟最常见的选择
- **6 人以上或大地图**：8 核 16G，别在 4 核 16G 上纠结太久
- **多地图互联**：按每图 6G 累加，直接跳到高内存档位

下单前确认两件事：**一是你的机型能不能自己加 UDP 端口映射**（NAT 型必须能加 7777、7778、27015 三条）；**二是磁盘给 30G 够不够**，取决于你装不装 MOD、开几张图，拿不准就往大了留。

雨云的新用户注册后绑定微信通常能领到首月折扣券，具体力度和有效期以官网活动页为准：👉 [从雨云挑一台合适的机器开始搭服](https://bit.ly/RaiNyun)
