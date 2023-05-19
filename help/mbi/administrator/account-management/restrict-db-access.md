---
title: 限制對資料庫的存取
description: 瞭解如何限制存取，限制對存放您資料庫的伺服器的存取。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 限制存取

當您建立與伺服器的SSH通道時，不需要 [!DNL Adobe Commerce Intelligence] 以存取資料庫以外的任何專案。 如果您不想 [!DNL Commerce Intelligence] 若要完整存取存放您資料庫的伺服器，您可以透過強制 [!DNL Commerce Intelligence Linux] 使用者進入 [受限的破折號殼層](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

您可能從名稱猜到了，但使用受限的bash shell來設定比標準shell更受控制的環境。 這類殼層的重要一點在於，受限殼層使用者無法存取系統功能或進行任何型別的修改。

若要限制 [!DNL Commerce Intelligence Linux] 使用者，您必須執行下列兩件事：

1. 將PATH環境變數變更為空字串。 這表示使用者無法存取系統可執行檔。

1. 請確定執行的Shell為 `bash -r`

這兩項作業都可以在內完成 `authorized_keys` 檔案於使用者首頁 `dir/.ssh` 目錄，作為使用者登入時所執行命令的一部分。 它看起來像這樣：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成時，您為建立的使用者 [!DNL Commerce Intelligence] 無法變更您的系統。
