---
title: 透過SSH通道連線PostgreSQL
description: 瞭解如何透過SSH通道將PostgreSQL資料庫連結至Commerce Intelligence。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Connect [!DNL PostgreSQL] 透過 [!DNL SSH Tunnel]

若要連線您的 [!DNL PostgreSQL] 資料庫至 [!DNL Commerce Intelligence] 透過 `SSH tunnel`，您必須執行下列動作：

1. [擷取 [!DNL Commerce Intelligence] 公開金鑰](#retrieve)
1. [允許存取 [!DNL Commerce Intelligence] ip位址](#allowlist)
1. [建立 [!DNL Linux] 使用者 [!DNL Commerce Intelligence] ](#linux)
1. [建立 [!DNL PostgreSQL] 使用者 [!DNL Commerce Intelligence] ](#postgres)
1. [將連線和使用者資訊輸入到 [!DNL Commerce Intelligence]](#finish)

## 正在擷取 [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

此 `public key` 用於授權 [!DNL Commerce Intelligence] [!DNL Linux] 使用者。 現在，您將建立使用者並匯入金鑰。

1. 前往 **[!UICONTROL Manage Data** > **Connections]** 並按一下 **[!UICONTROL Add a Data Source]**.
1. 按一下 [!DNL PostgreSQL] 圖示。
1. 晚於 `PostgreSQL credentials` 頁面開啟，設定 `Encrypted` 切換至 `Yes`. 這會顯示 `SSH` 設定表單。
1. 此 `public key` 位於此表單下方。

在本教學課程中保持此頁面開啟 — 您需要在下一節和結尾使用它。

以下示範如何瀏覽 [!DNL Commerce Intelligence] 擷取金鑰：

![正在擷取RJMetrics公開金鑰](../../../assets/get-mbi-public-key.gif)

## 允許存取 [!DNL Commerce Intelligence] ip位址 {#allowlist}

若要讓連線成功，您必須將防火牆設定為允許從IP位址存取。 它是 `54.88.76.97/32`，但也位在 `PostgreSQL` 認證頁面。 請參閱上方GIF中的藍色方塊。

## 建立 [!DNL Linux] 使用者 [!DNL Commerce Intelligence] {#linux}

這可以是生產或次要機器，只要它包含即時（或經常更新）資料即可。 您可以 [限制此使用者](../../../administrator/account-management/restrict-db-access.md) 任何您喜歡的方式，只要它保留連線至 [!DNL PostgreSQL] 伺服器。

1. 若要新增使用者，請以root身分在 [!DNL Linux] 伺服器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 記住 `public key` 您在第一節中擷取了嗎？ 為確保使用者有權存取資料庫，您需要將金鑰匯入 `authorized\_keys`.

   將整個金鑰複製到 `authorized\_keys` 檔案如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 若要完成建立使用者，請變更以下專案的許可權： `/home/rjmetric` 允許透過存取的目錄 `SSH`：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 與伺服器關聯的檔案未設定為預設選項，只有特定使用者擁有伺服器存取權 — 這會防止成功連線至 [!DNL Commerce Intelligence]. 在這些情況下，必須執行命令，例如 `AllowUsers` 允許rjmetric使用者存取伺服器。

## 建立 [!DNL Commerce Intelligence] [!DNL Postgres] 使用者 {#postgres}

您的組織可能需要不同的程式，但建立此使用者最簡單的方法是在以有權授予許可權的使用者身分登入Postgres時執行以下查詢。 該使用者也應擁有以下專案的結構描述： [!DNL Commerce Intelligence] 正在被授予存取權。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Replace `secure password` 使用您自己的安全密碼，此密碼可不同於SSH密碼。 此外，請務必取代 `database name` 和 `schema name` 在資料庫中使用適當的名稱。

如果要連線多個資料庫或結構描述，請視需要重複此程式。

## 將連線和使用者資訊輸入到 [!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須將連線和使用者資訊輸入到 [!DNL Commerce Intelligence]. 您是否離開 [!DNL PostgreSQL] 憑證頁面是否開啟？ 如果沒有，請前往 **[!UICONTROL Manage Data > Connections]** 並按一下 **[!UICONTROL Add a Data Source]**，然後 [!DNL PostgreSQL] 圖示。 別忘了設定 `Encrypted` 切換至 `Yes`.

在此頁面中輸入下列資訊，從 `Database Connection` 區段：

* `Username`： RJMetrics Postgres使用者名稱（應為rjmetric）
* `Password`： RJMetrics Postgres密碼
* `Port`：伺服器上的PostgreSQL連線埠（預設為5432）
* `Host`: 127.0.0.1

下 `SSH Connection`：

* `Remote Address`：您要透過SSH連線的伺服器IP位址或主機名稱
* `Username`：您的SSH登入名稱（應為rjmetric）
* `SSH Port`：伺服器上的SSH連線埠（預設為22）

完成後，按一下 **儲存並測試** 以完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
