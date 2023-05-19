---
title: Google Analytics — 追蹤資料庫中的使用者裝置和瀏覽器資料
description: 瞭解實際有多少使用者透過行動裝置登入，以及這如何影響這些使用者的期限值。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] 追蹤

替換為 [!UICONTROL Google Analytics] 您可以 [儲存反向連結來源資訊](../analysis/google-track-user-acq.md) 瞭解您最有價值的使用者來自何處。 本主題說明使用者所使用的平台（例如裝置或瀏覽器）。 透過此專案，您將能夠瞭解實際上有多少使用者正透過行動裝置登入，以及這如何影響這些使用者的期限值。

## 儲存使用者裝置和瀏覽器資料

每次向您的網站提出請求時，使用者的瀏覽器都會傳送使用者代理字串，其中包含提出請求的平台的相關資訊。 以下是使用者代理字串的一些範例：

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

如果您仔細檢視，會發現字串包含使用者作業系統、瀏覽器及其使用裝置名稱（如果有的話）的相關資訊。 雖然使用者代理字串在各平台之間甚至同一平台的版本之間差異極大，但平台名稱通常確實會存在於其內部。 例如，上#1是具有Chrome瀏覽器的Mac，#2上則是具有Firefox瀏覽器的Windows電腦、#3是iPhone、#4是iPad，#5是Android裝置。

每次提出請求時，您的伺服器都能存取此資訊。 在PHP中，使用者代理字串儲存在 `$_SERVER['HTTP_USER_AGENT']`. 在Ruby on Rails中，儲存在 `request.env['HTTP_USER_AGENT']`. 其他語言和環境可讓您以類似方式存取它。

### 您何時應該記錄此資料？

[!DNL Adobe] 建議您新增欄位 `Platform` 或 `User-Agent` 至您的 `Customers` 和 `Orders` 建立使用者或下訂單時儲存此資訊的資料庫表格。 如果您使用SQL資料庫，此欄位應該是 `VARCHAR(255)`. 

>[!NOTE]
>
>此 `User-Agent` 字串的長度允許超過此長度，但實際上很少超過此長度。

### 如何剖析有用的區段？

有許多程式庫可協助您剖析 `User-Agent` 字串輸入作業系統、裝置等元件中。 請參閱 [ua-parser專案](https://github.com/tobie/ua-parser) 以深入瞭解。

有了這項新資訊，您就能更清楚瞭解使用者如何存取您的網站。 然後，您可以量身打造其體驗，或為特定群組建立行銷活動。

## 相關

* [透過以下方式追蹤訂單反向連結來源： [!DNL Google Anaytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因是否有效？](../analysis/utm-attributes.md)
