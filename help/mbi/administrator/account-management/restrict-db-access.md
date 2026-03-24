---
title: 限制对数据库的访问
description: 了解如何限制访问，限制对存放数据库的服务器的访问。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
TQID: https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 204
ht-degree: 0%

---

# 限制访问

创建到服务器的SSH通道时，[!DNL Adobe Commerce Intelligence]不需要访问除数据库之外的任何内容。 如果不希望[!DNL Commerce Intelligence]对存放数据库的服务器具有完全访问权限，则可以通过强制[!DNL Commerce Intelligence Linux]用户进入[受限的bash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)来限制访问权限。

您可能从名称猜到了，但使用受限的bash shell设置比标准shell更受控制的环境。 这种外壳的重要之处在于，受限外壳用户无法访问系统功能或进行任何类型的修改。

要限制[!DNL Commerce Intelligence Linux]用户，您必须执行两项操作：

1. 将PATH环境变量更改为空字符串。 这意味着用户无法访问系统可执行文件。

1. 确保执行的shell为`bash -r`

这两项操作都可以在用户主`authorized_keys`目录中的`dir/.ssh`文件内完成，作为用户登录时执行的命令的一部分。 它看起来像这样：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成后，您为[!DNL Commerce Intelligence]创建的用户无法更改您的系统。
