---
title: MongoDB数据建模
description: 了解如何避免数据模式会导致问题。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# [!DNL MongoDB] 数据建模

When [!DNL MBI] 拉进 [!DNL MongoDB] 数据，该数据被转换为关系模型。

坏消息是：虽然大多数数据模式并不构成问题，但由于转换到关系模型，有少数数据模式， [!DNL MBI] 不支持。

好消息是：所有这些模式都可以避免。

## 子嵌套数组 {#subnested}

如果您的收藏集类似于以下示例， [!DNL MBI] 将仅复制项目数组中的数据。 将不会提取子项目数组中的数据。

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## 变量对象键 {#varobjectkeys}

在中不会复制包含具有变量对象键的对象的集合 [!DNL MBI]. 例如：

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

这通常发生在使用对象且数组更合适的情况下。 现在，我们将重新编写上述示例：

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
