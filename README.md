# 开源背景

在《幻兽帕鲁》大火之后，阿里云基于计算巢提供的[一键搭建幻兽帕鲁游戏服务器的服务模板](https://computenest.aliyun.com/services/detail?serviceId=service-f99b27842d464c02846f)帮助了很多不熟悉服务器运维的玩家搭建自己的幻兽帕鲁游戏服务器。玩家不再需要关注服务器的购买、网络端口设置、防火墙配置、游戏环境安装等操作。为了给玩家带来极致体验，计算巢团队在 2 周内对幻兽帕鲁快速部署服务迭代了 90 个版本，支持了界面化配置游戏参数、管理存档、设置定时重启等功能。

为了帮助更多开发者、软件厂商、游戏厂商了解计算巢，并通过计算巢服务客户获得收益，阿里云决定将一键搭建幻兽帕鲁服务器的计算巢服务模板代码开源，供大家参考。

当然，您也可以基于这个服务模板继续改进，提供体验更好、功能更强大的幻兽帕鲁服务器代部署服务。

# 什么是计算巢？

[计算巢](https://www.aliyun.com/product/computenest)是面向服务商和开发者的一站式软件云化平台，构建云原生 SaaS，完成传统软件 SaaS 化。助力其提升软件服务在交付、部署及后续管理的效率，为用户提供一站式订阅和自动化部署的软件服务，打造更高效、便捷、安全的使用体验。

# 工作原理

在阿里云提供的一键搭建幻兽帕鲁服务器服务中，包含两类关键模板：

*   [服务主模板](https://github.com/aliyun-computenest/quickstart-palo-world/blob/main/templates/template.yaml)是阿里云资源编排（ROS）模板，主要作用是帮助用户自动化创建云资源、配置云资源、安装幻兽帕鲁游戏服务端软件。
    
*   [运维模板](https://github.com/aliyun-computenest/quickstart-palo-world/tree/main/templates/operation)是阿里云系统运维管理（OOS）模板，主要作用是在幻兽帕鲁游戏服务器搭建完成后，提供界面化的自动重启、导入存档等功能。
    

# 在计算巢上创建并发布服务的步骤

这里，我们以发布一个一键搭建幻兽帕鲁游戏服务器的计算巢服务为例，演示如何在计算巢上创建并发布您的服务。

## 步骤 1：选择服务创建模式

登录[计算巢控制台](https://computenest.console.aliyun.com/service/)。在**我的服务**页面，点击**创建服务**按钮，选择**自定义创建服务**，选择**私有部署服务**，进入服务创建流程。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/02bfb5f2-e43b-47a2-8629-c2004b047bbf.png?x-oss-process=image/crop,x_0,y_33,w_1192,h_651)

## 步骤 2：填写服务基础信息

按界面提示，上传**服务图标**，填写**服务名称**、**服务简介**和**版本描述**。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/4bf40517-ced0-4b68-86f5-69d3db4139ac.png)

## 步骤 3：填写服务部署信息

1.  选择部署地域，使用**template.yaml**文件完成手动录入模板。  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/6804855e-dbdd-424b-af49-b4cdc0aa884f.png)  
    **template.yaml**文件的位置和内容如下图所示：  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/2c691162-0d5f-4981-8fad-4bb6d3dd2ecc.png)
    
2.  创建帕鲁服务的套餐，不同套餐可以选择不同服务配置进行收费。套餐参考如下：  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/3b4845cc-88e4-44f9-8704-41901061d3b0.png)
    
3.  关联游戏镜像的部署物，此处的镜像部署物需要单独创建。
    

1.  自定义镜像：可以在[ECS镜像的控制台](https://ecs.console.aliyun.com/image/region/cn-hangzhou/imageList)创建。  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/38fd1ff4-7aac-46af-bac8-03ea95f23e14.png)
    
2.  镜像部署物：完成自定义镜像创建后，可以在[计算巢部署物管理界面](https://computenest.console.aliyun.com/artifact/create/cn-hangzhou)进行创建。  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/0c275c7a-a6f5-496f-986e-62e1886fba66.png)
    
3.  回到计算巢服务创建流程中，关联镜像部署物。  
    ![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/b91fa88a-a8ba-4f06-a998-c4cf623f42d8.png)
    

执行到此步骤，您已完成填写幻兽帕鲁计算巢服务的基本部署信息。

## （可选）步骤 4：填写服务运维信息

在服务创建流程中，计算巢还提供了自定义运维操作的功能，您可以点击**添加自定义运维操作**按钮使用OOS模板自定义运维操作。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/1f1349c6-1b7d-47d0-96a4-a4bdcd4f0eca.png)

本仓库为大家开源了多个运维操作的服务模板，只需要将对应的文件粘贴到上面的相应位置即可。您可以考虑自行修改运维操作。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/8e15615b-dc96-49d1-a2bc-9dc6322b5245.png)

完成添加后，我们将获得对幻兽帕鲁服务的多个运维项操作。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/b710c7cc-0806-473c-baa7-6952d156ff9e.png)

后续在创建幻兽帕鲁服务实例的时候，游戏玩家就可以直接对服务进行运维操作了，以下是操作界面示例。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/446b5d8d-a2c8-41be-9a7e-cba19a3c6392.png)

完成运维项填写后，计算巢还提供了一些其他功能，例如监控、日志等，这些配置您可按需自定义。

## （可选）步骤 5：填写高级配置信息

计算巢提供了高级配置功能，例如试用、网络和分销等。针对部署幻兽帕鲁的游戏服务，这些功能不建议配置，直接点击服务发布即可。

## 步骤 6：发布服务

点击**预发布**后，服务将会进入审核，官方审核通过后，用户可以直接打开访问。到这里服务就已经创建完成了，

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/09d11507-ec45-48f4-879a-bba24e69f391.png)

在**我的服务**列表，可以看到您刚创建的服务。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/892efa55-424c-47c7-84b2-39347b9a942e.png)

## 验证：使用服务创建游戏云服务器

在**服务详情**页，点击**用户部署链接**打开幻兽帕鲁的服务创建页面。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/2bb8f610-8dda-49c0-b301-f8df5b3dcac6.png)

在该页面，只要下单完成购买，就能获得一台运行帕鲁游戏的服务器了。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/b0ee0ba3-6d28-4dce-a155-bd0a286aebba.png)

购买成功后将获得服务实例，界面如下，可以看到之前定义的运维操作等功能。通过服务器地址端口就可以直接开启快乐的游戏了～

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/658af8c1-df2f-4991-8893-11402392d129.png)

# 问题交流

有任何游戏问题和服务部署问题，欢迎大家钉钉扫码加入我们的开发者服务群。

也可以钉钉搜索群号加入（群号：75685004710）。

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1X3lE6EA9jV6nJbv/img/f0307912-76b1-41d8-8bcb-e0724419a94d.png)