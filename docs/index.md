# 计算巢1分钟部署幻兽帕鲁联机服务

## 概述

	幻兽帕鲁是Pocketpair开发的一款开放世界生存制作游戏，游戏于2024年1月18日发行抢先体验版本。游戏中，玩家可以在广阔的世界中收集神奇的生物“帕鲁”，派他们进行战斗、建造、做农活，工业生产等。本文介绍如何在阿里云计算巢控制台，快速部署幻兽帕鲁联机服务，实现和朋友一起联机游戏。
	预计部署时间1~2分钟，有任何问题请查看文档底部的微信二维码，进群交流～

## 计费说明

幻兽帕鲁联机服务在计算巢上的费用主要涉及：

- 所选vCPU与内存规格
- 磁盘容量
- 公网带宽

计费方式包括：

- 按量付费（小时）
- 包年包月

预估费用在创建实例时可实时看到。

## 部署架构

幻兽帕鲁联机服务是单机部署架构

## RAM账号所需权限

幻兽帕鲁联机服务需要对ECS、VPC等资源进行访问和创建操作，若您使用RAM用户创建服务实例，需要在创建服务实例前，对使用的RAM用户的账号添加相应资源的权限。添加RAM权限的详细操作，请参见[为RAM用户授权](https://help.aliyun.com/document_detail/121945.html)
。所需权限如下表所示。

| 权限策略名称                          | 备注                         |
|---------------------------------|----------------------------|
| AliyunECSFullAccess             | 管理云服务器服务（ECS）的权限           |
| AliyunVPCFullAccess             | 管理专有网络（VPC）的权限             |
| AliyunROSFullAccess             | 管理资源编排服务（ROS）的权限           |
| AliyunComputeNestUserFullAccess | 管理计算巢服务（ComputeNest）的用户侧权限 |
| AliyunCloudMonitorFullAccess    | 管理云监控（CloudMonitor）的权限     |

## 部署流程

### 部署服务

1. 第一步：创建服务实例，创建服务实例。
   点击上方按钮“正式创建”，或单击[部署链接](https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-f99b27842d464c02846f)，进入服务实例部署界面，根据界面提示和自己的需求，选择相应套餐。
   ![1.jpg](1.jpg)

2. 第二步：确认订单费用，完成支付。
   查看订单资源和相关费用，勾选服务协议，确认后点击“立即创建”。
   ![22.jpg](22.jpg)

3. 第三步：查看服务实例列表。
   等待创建成功后，点击“去列表查看”，来到服务实例列表。可看到服务实例已经创建，点击红色方框处，进入服务实例详情页。
   ![33.jpg](33.jpg)

4. 第4步：查看服务实例详情，”立即使用”。
   进入服务实例详情后，等到服务实例创建完成后，在”立即使用”一栏，获取幻兽帕鲁服务器地址端口，此时服务器已经部署完成，可以去登录游戏了。
   ![2.jpg](2.jpg)

### 登录游戏

前置条件：您首先需要在Steam购买幻兽帕鲁（Palworld）。

1. 登录您的Steam账号。

   ![3.jpg](3.png)

2. 在“库”中找到幻兽帕鲁，并开始游戏。
   ![4.jpg](4.png)

3. 在游戏菜单选择“加入多人游戏（专用服务器）”
   ![5.jpg](5.png)

4. 让玩家输入您已部署的计算巢服务实例的地址端口即可畅快开玩～
   ![6.jpg](6.png)

至此，您已经成功搭建了幻兽帕鲁 Dedicated Server ，请和您的朋友在此中一起畅快游玩吧～

### 管理存档

如果你原来在本地或者其他地方搭建过 Palworld 服务器，希望把存档转移到云服务器上，可以把对应的存档文件拷贝到对应的位置：
   ```
   /home/ecs-assist-user/.steam/SteamApps/common/PalServer/Pal/Saved/SaveGames
   ```
然后重启服务：
  ```
  systemctl restart pal-server
  ```

### 修改配置

1. 远程连接ECS实例

   ![10.jpg](10.jpg)

2. 编辑文件

   ```
   # 修改前注意备份
   cp /home/ecs-assist-user/.steam/SteamApps/common/PalServer/DefaultPalWorldSettings.ini /home/ecs-assist-user/.steam/SteamApps/common/PalServer/Pal/Saved/Config/LinuxServer/PalWorldSettings.ini
   ``` 
   
   ```
   # 修改配置
   vim /home/ecs-assist-user/.steam/SteamApps/common/PalServer/Pal/Saved/Config/LinuxServer/PalWorldSettings.ini 
   ```
   ![11.jpg](11.jpg)
   修改完对应配置参数后保存：
   ![12.jpg](12.jpg)

   ```
   # 修改完成后重启服务
   sudo systemctl restart pal-server
   ```
   配置文件参数说明:

| Difficulty                         | 英文                                                                                                                                                              | 机翻                                                                                      |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| DayTimeSpeedRate                   | Day time speed                                                                                                                                                  | 白天速度                                                                                    |
| NightTimeSpeedRate                 | Night time speed                                                                                                                                                | 夜间速度                                                                                    |
| ExpRate                            | EXP rate                                                                                                                                                        | 经验率                                                                                     |
| PalCaptureRate                     | Pal capture rate                                                                                                                                                | 好友捕获率                                                                                   |
| PalSpawnNumRate                    | Pal appearance rate                                                                                                                                             | Pal出现率                                                                                  |
| PalDamageRateAttack                | Damage from pals multipiler                                                                                                                                     | 好友倍增器造成的伤害                                                                              |
| PalDamageRateDefense               | Damage to pals multipiler                                                                                                                                       | 对好友倍增器造成伤害                                                                              |
| PlayerDamageRateAttack             | Damage from player multipiler                                                                                                                                   | 玩家倍增造成的伤害                                                                               |
| PlayerDamageRateDefense            | Damage to player multipiler                                                                                                                                     | 对玩家造成的伤害乘数                                                                              |
| PlayerStomachDecreaceRate          | Player hunger depletion rate                                                                                                                                    | 玩家饥饿消耗率                                                                                 |
| PlayerStaminaDecreaceRate          | Player stamina reduction rate                                                                                                                                   | 玩家体力减少率                                                                                 |
| PlayerAutoHPRegeneRate             | Player auto HP regeneration rate                                                                                                                                | 玩家自动HP回复率                                                                               |
| PlayerAutoHpRegeneRateInSleep      | Player sleep HP regeneration rate                                                                                                                               | 玩家睡眠HP回复率                                                                               |
| PalStomachDecreaceRate             | Pal hunger depletion rate                                                                                                                                       | 伙伴饥饿消耗率                                                                                 |
| PalStaminaDecreaceRate             | Pal stamina reduction rate                                                                                                                                      | 帕尔耐力减少率                                                                                 |
| PalAutoHPRegeneRate                | Pal auto HP regeneration rate                                                                                                                                   | Pal自动HP回复率                                                                              |
| PalAutoHpRegeneRateInSleep         | Pal sleep health regeneration rate (in Palbox)                                                                                                                  | Pal 睡眠健康恢复率（Palbox 中）                                                                   |
| BuildObjectDamageRate              | Damage to structure multipiler                                                                                                                                  | 多层结构损坏                                                                                  |
| BuildObjectDeteriorationDamageRate | Structure determination rate                                                                                                                                    | 结构测定率                                                                                   |
| CollectionDropRate                 | Getherable items multipiler                                                                                                                                     | 可收集物品倍增器                                                                                |
| CollectionObjectHpRate             | Getherable objects HP multipiler                                                                                                                                | 可收集的物体 HP 倍增器                                                                           |
| CollectionObjectRespawnSpeedRate   | Getherable objects respawn interval                                                                                                                             | 可收集物体的重生间隔                                                                              |
| EnemyDropItemRate                  | Dropped Items Multipiler                                                                                                                                        | 掉落物品倍增器                                                                                 |
| DeathPenalty                       | Death penalty None : No lost, Item : Lost item without equipment, ItemAndEquipment : Lost item and equipment, All : Lost All item, equipment, pal(in inventory) | 死刑 None : 没有丢失， Item : 丢失的没有装备的物品， ItemAndEquipment : 丢失的物品和装备， All : 丢失所有物品、装备、朋友（库存中） |
| GuildPlayerMaxNum                  | Max player of Guild                                                                                                                                             | 公会最大玩家数                                                                                 |
| PalEggDefaultHatchingTime          | Time(h) to incubate massive egg                                                                                                                                 | 孵化大蛋的时间(h)                                                                              |
| ServerPlayerMaxNum                 | Maximum number of people who can join the server                                                                                                                | 服务器最多可加入人数                                                                              |
| ServerName                         | Server name                                                                                                                                                     | 服务器名称                                                                                   |
| ServerDescription                  | Server description                                                                                                                                              | 服务器描述                                                                                   |
| AdminPassword                      | AdminPassword                                                                                                                                                   | 管理员密码                                                                                   |
| ServerPassword                     | Set the server password                                                                                                                                         | 设置服务器密码                                                                                 |
| PublicPort                         | Public port number                                                                                                                                              | 公共端口号                                                                                   |
| PublicIP                           | Public IP                                                                                                                                                       | 公共IP                                                                                    |
| RCONEnabled                        | Enable RCON                                                                                                                                                     | 启用RCON                                                                                  |
| RCONPort                           | Port number for RCON                                                                                                                                            | RCON 的端口号                                                                               |

## 节约成本

前提条件： 部署服务时计费方式选择****按量付费****

使用完毕后可以通过下述两种方式来节省成本：

1. 若只是暂时不使用了可以在运维管理页面选择关机（节省停机模式），此时部分资源会被回收并停止收费，以降低相关费用、节约使用成本，下次使用再进行开机，操作如下：
   ![8.jpg](8.jpg)
2. 若彻底不再使用了可以直接将服务实例删除，后续就不会再产生费用
   ![9.jpg](9.jpg)

## 服务支持

您有任何问题或者建议，可以使用微信扫描二维码，加人我们的官方服务群，我们将非常欢迎您的建议和反馈～

<img src="7.png" width="300" height="350" align="bottom"/>
