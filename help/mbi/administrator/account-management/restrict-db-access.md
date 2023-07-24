---
title: 限制对数据库的访问
description: 了解如何限制访问，限制对存放数据库的服务器的访问。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 限制访问

创建到服务器的SSH隧道时，不需要 [!DNL Adobe Commerce Intelligence] 除了数据库之外，任何东西都可以访问。 如果你不想 [!DNL Commerce Intelligence] 要完全访问存放数据库的服务器，您可以通过强制 [!DNL Commerce Intelligence Linux] 用户进入 [受限的垃圾桶](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

您可能从名称猜到了，但使用受限制的bash shell设置比标准shell控制得更好的环境。 此类外壳的重要特性是受限制的外壳用户无法访问系统功能或进行任何类型的修改。

要限制 [!DNL Commerce Intelligence Linux] 用户，您必须执行以下两项操作：

1. 将PATH环境变量更改为空字符串。 这意味着用户无法访问系统可执行文件。

1. 确保执行的shell为 `bash -r`

这两项操作均可在 `authorized_keys` 用户主页中的文件 `dir/.ssh` 目录，作为用户登录时执行的命令的一部分。 它看起来像这样：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成后，您为创建的用户 [!DNL Commerce Intelligence] 无法更改您的系统。
