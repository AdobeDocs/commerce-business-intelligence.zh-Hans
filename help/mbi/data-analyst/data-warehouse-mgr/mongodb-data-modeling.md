---
title: MongoDB数据建模
description: 了解如何避免产生问题的数据模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# [!DNL MongoDB]数据建模

当[!DNL Adobe Commerce Intelligence]拉入[!DNL MongoDB]数据时，该数据将转换为关系模型。

坏消息：虽然大多数数据模式不会造成问题，但有一些模式不受[!DNL Commerce Intelligence]支持，因为转换为关系模型。

好消息是，所有这些模式都可以避免。

## 子嵌套数组 {#subnested}

如果您的集合与以下示例类似，[!DNL Commerce Intelligence]仅复制项数组中的数据。 不提取子项数组中的数据。

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

## 可变对象键 {#varobjectkeys}

包含具有可变对象键的对象的集合未在[!DNL Commerce Intelligence]中复制。 例如：

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

这通常发生在使用对象并且数组更合适的地方。 现在，重新制作上面的示例：

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
