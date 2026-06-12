---
title: SSH主机密钥验证
description: 了解Commerce Intelligence如何注册SSH主机密钥、如何刷新这些密钥、排查错误以及何时联系支持人员以获取SSH通道连接。
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# SSH主机密钥验证 {#ssh-host-keys}

[!DNL Commerce Intelligence]对加密（SSH通道）数据库连接（包括[MySQL](mysql-via-ssh-tunnel.md)、[MongoDB](mongodb-via-ssh-tunnel.md)和[PostgreSQL](postgresql.md)）使用严格的SSH主机密钥验证。

在&#x200B;**[!UICONTROL Save & Test]**&#x200B;期间，系统会为您的连接注册SSH堡垒主机密钥，并在每个连接中安全地存储这些密钥。 注册后，只有当live bastion主机密钥与注册的密钥匹配时，复制和隧道才成功。

该模型通过阻止中间人攻击和意外的主机更改来提高安全性。 这也意味着主机密钥轮换、缺少信任材料或基础架构更改可能会显示为连接上的SSH主机密钥错误，而不是一般的隧道故障。

>[!NOTE]
>
>**管理员**&#x200B;是指对您的[!DNL Commerce Intelligence]帐户拥有管理员权限的用户，除非另有说明，否则不是您的Adobe组织控制台。 只有管理员可以运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 如果未看到此控件，请要求您帐户中的管理员运行刷新或联系Adobe支持部门。

您不编辑、上传或管理`known_hosts`文件。 在分配给您帐户的Adobe基础架构上注册并刷新运行。

>[!IMPORTANT]
>
>主机密钥轮换需要管理员才能运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 如果更改了堡垒主机密钥或更改了堡垒标识（主机名、IP或端口），则再次运行&#x200B;**[!UICONTROL Save & Test]**&#x200B;或重新保存连接不会更新已注册的密钥。 在管理员刷新主机密钥之前，连接可能会一直失败。

## 保存并测试 {#save-and-test}

**[!UICONTROL Save & Test]**&#x200B;仅执行&#x200B;**初始SSH主机密钥注册**。 该键在设计上较为保守，不会旋转或覆盖已注册连接的键。

| 已注册的主机密钥状态 | 保存和测试的作用 |
| --- | --- |
| 尚未注册主机密钥 | **[!UICONTROL Save & Test]**&#x200B;扫描堡垒主机和端口，注册主机密钥，并存储它们以便进行此连接。 |
| 已注册主机密钥 | **[!UICONTROL Save & Test]**&#x200B;跳过注册。 它不会覆盖、旋转或删除现有的已注册键，即使实时键不再匹配也是如此。 |
| 已注册密钥缺失、空或无效 | **[!UICONTROL Save & Test]**&#x200B;本身不会修复无效的信任材料。 管理员必须运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，如果错误继续存在，请联系支持人员 |

成功完成首次注册后，**[!UICONTROL Save & Test]**&#x200B;稍后将运行验证凭据和连接设置，但保留已注册的SSH主机密钥不变。

## 刷新SSH主机密钥 {#refresh-ssh-host-keys}

当堡垒已更改或必须修复信任材料时，**[!UICONTROL Refresh SSH Host Keys]**&#x200B;更新已注册SSH主机密钥。 管理员从&#x200B;**[!UICONTROL Data]** > **[!UICONTROL Connections]**&#x200B;中的连接开始刷新。

刷新在分配给您帐户的Adobe基础架构上异步运行。 [!DNL Commerce Intelligence]在刷新排入队列后返回。 它不会在您的工作站上运行扫描。

仅当下列条件之一为true时，刷新&#x200B;**重写已注册的主机密钥**：

* 缺少已注册的主机键
* 已注册的主机密钥为空
* 无法读取已注册的主机密钥
* 注册的主机密钥验证失败
* 新扫描返回的主机键行与已注册的键不同
* 扫描密钥和已注册密钥中的指纹不匹配

如果注册的密钥是最新的且有效，则刷新完成时不会更改它们。

>[!TIP]
>
>在团队旋转堡垒上的SSH主机密钥、更改堡垒主机名或IP或替换SSH端点后，运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 等待几分钟，然后运行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以确认连接。

## 帐户迁移 {#migration}

您不会触发帐户迁移。 Adobe在维护或扩展期间执行数据服务器移动，并复制已注册的SSH主机密钥，以便在移动后继续使用严格验证。

在Adobe通知您迁移已完成后：

1. 运行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以确认连接。 如果成功复制了密钥，则应跳过注册。
1. 如果SSH主机密钥错误仍然存在，请要求管理员运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等待几分钟，然后再次运行&#x200B;**[!UICONTROL Save & Test]**。
1. 如果在尝试&#x200B;**[!UICONTROL Save & Test]**&#x200B;和最多两次&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;次后错误继续出现，请联系Adobe支持。

## SSH主机密钥错误消息 {#ssh-host-key-errors}

连接状态显示一条用户友好的SSH主机密钥消息。 原始的OpenSSH错误不会显示在仪表板中。

下表将常见消息映射到可能的原因和典型的后续步骤。

| 消息或状态 | 它的含义 | 可能的原因 | 典型下一步 |
| --- | --- | --- | --- |
| SSH主机密钥验证失败 | 堡垒主机密钥与已注册的密钥不匹配，或信任材料不可用 | 在堡垒上轮换的SSH主机密钥；堡垒主机名、IP或端口已更改；注册的密钥缺失、为空、无效或无法读取 | 确认&#x200B;**远程地址**&#x200B;和&#x200B;**SSH端口**。 询问您的基础架构团队是否更改了堡垒主机密钥。 要求管理员运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等待几分钟，然后运行&#x200B;**[!UICONTROL Save & Test]**。 |
| 无法注册SSH主机密钥 | **[!UICONTROL Save & Test]**&#x200B;无法扫描或存储备用主机密钥 | 无法从Adobe基础结构访问堡垒；DNS失败；防火墙阻止[!DNL Commerce Intelligence]个IP地址；错误的&#x200B;**远程地址**&#x200B;或&#x200B;**SSH端口**；堡垒上的主机密钥扫描失败 | 在数据库凭据页面上使用[!DNL Commerce Intelligence] IP地址验证防火墙列入允许列表。 确认堡垒在配置的端口上接受SSH。 更正连接字段并重新运行&#x200B;**[!UICONTROL Save & Test]**。 |
| SSH主机密钥缺失或无效 | 严格验证阻止了通道，因为已注册的信任材料不存在或已损坏 | 第一个连接从未完成注册；先前刷新失败；迁移未复制密钥；Adobe基础架构出现问题 | 要求管理员运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，然后再运行&#x200B;**[!UICONTROL Save & Test]**。 如果错误仍然存在，请联系支持人员。 |
| 无法完成刷新SSH主机密钥 | 刷新未更新已注册的密钥 | 刷新期间网络、DNS或扫描失败；Adobe基础架构上出现问题 | 等待几分钟。 要求管理员再次运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**（如果第一次尝试失败，则第二次尝试）。 确认堡垒可达性和列入允许列表。 如果连接在两次刷新尝试和&#x200B;**[!UICONTROL Save & Test]**&#x200B;后仍然失败，请联系支持人员。 |

## 故障排除清单 {#troubleshooting}

1. 确认&#x200B;**远程地址**、**SSH端口**&#x200B;和Linux用户设置与您的堡垒设置相匹配。
1. 确认防火墙允许数据库凭据页面上显示的[!DNL Commerce Intelligence]个IP地址。
1. 询问您的基础架构团队最近是否更改了堡垒上的SSH主机密钥。
1. 运行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以验证设置并注册密钥（如果尚未存在）。
1. 要求管理员运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等待几分钟，然后再次运行&#x200B;**[!UICONTROL Save & Test]**。 如果首次刷新不能解决错误，请重复此步骤。
1. 如果连接在两次刷新尝试后仍显示SSH主机密钥错误，请在连接页面（或您的帐户支持渠道）上单击&#x200B;**[!UICONTROL Contact Support]**。

## 何时联系Adobe支持 {#contact-support}

在以下情况下联系支持人员：

* SSH主机密钥错误在管理员运行两次&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;后继续出现，并且&#x200B;**[!UICONTROL Save & Test]**&#x200B;仍然失败
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;从不完成，或连接状态在15-30分钟后未更改
* Adobe通知您帐户迁移或数据服务器维护后，立即开始出现错误
* 堡垒设置和防火墙列入允许列表正确，您的团队未轮换主机密钥，您仍然无法连接
* 您需要管理员才能运行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，但此帐户中没有可用的管理员

包括连接名称、上次&#x200B;**[!UICONTROL Save & Test]**&#x200B;或刷新尝试的大致时间，以及是否最近更改了堡垒主机密钥。 请勿发送私钥或密码。

## 相关 {#related}

* [通过SSH通道连接MySQL](mysql-via-ssh-tunnel.md)
* [通过SSH隧道连接MongoDB](mongodb-via-ssh-tunnel.md)
* [通过SSH通道连接PostgreSQL](postgresql.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
