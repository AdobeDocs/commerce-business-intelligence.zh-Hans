---
title: 限制对数据库的访问
description: 了解如何限制访问，以限制对存储数据库的服务器的访问。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# 限制访问

在创建到您服务器的SSH隧道时，无需 [!DNL MBI] 访问数据库以外的任何内容。 如果您不想 [!DNL MBI] 要拥有存储数据库的服务器的完全访问权限，可以通过强制 [!DNL MBI Linux] 用户 [受限制的击壳](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

您可能已经猜到了这个名称，但是，一个受限的bash shell用于设置一个比标准shell更受控制的环境。 这种Shell的重要之处在于，受限Shell用户不能访问系统功能或进行任何类型的修改。

要限制 [!DNL MBI Linux] 用户，您必须执行以下两项操作：

1. 将PATH环境变量更改为空字符串。 这意味着用户将无法访问系统可执行文件。

1. 确保执行的Shell为 `bash -r`

这两项操作都可以在 `authorized_keys` 文件 `dir/.ssh` 目录，作为用户登录时执行的命令的一部分。 它将如下所示：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成此操作后，您为 [!DNL MBI] 将无法对系统进行任何更改。
