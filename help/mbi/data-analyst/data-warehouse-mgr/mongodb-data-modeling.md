---
title: MongoDB数据建模
description: 了解如何避免产生问题的数据模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] 数据建模

时间 [!DNL MBI] 拉入 [!DNL MongoDB] 数据，该数据被转换为关系模型。

坏消息：虽然大多数数据模式并不构成问题，但因为转换为关系模型， [!DNL MBI] 不支持。

好消息是，所有这些模式都可以避免。

## 子嵌套数组 {#subnested}

如果您的收藏与以下示例类似， [!DNL MBI] 仅复制项目阵列中的数据。 不提取子项数组中的数据。

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

包含具有可变对象键的对象的集合不会在中复制 [!DNL MBI]. 例如：

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

这通常发生在使用对象的情况下，而数组更合适。 现在，重写上述示例：

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
