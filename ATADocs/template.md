---
# required metadata

title: [文章標題 | 服務名稱]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 中繼資料和 Markdown 範本

此 docs.ms 範本包含 Markdown 語法的範例，以及設定中繼資料的相關指引。 範本可在各個 EM 試驗儲存機制的根目錄 (例如 ~/Azure-RMSDocs-pr /template.md) 中取得，而且應讀取為 Markdown 檔案，不過您可以參考[發行的版本](https://stage.docs.microsoft.com/en-us/rights-management/template)以了解 Markdown 範例如何轉譯。

建立 Markdown 檔案時，您應該將範本複製到新的檔案，如下所指定填寫中繼資料，設定文章標題上方的 H1 標題，並刪除內容。 


## 中繼資料 

上方是完整的中繼資料區塊，分成必要的欄位和選用的欄位；如需詳細資訊，請參閱 [OPS 中繼資料速查表](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data)。 一些重點︰

- 在冒號 (:) 和中繼資料元素的值之間**必須**有一個空格。
- 如果選用的中繼資料元素沒有值，請以 # 將元元素註解化 (請勿保留空白或者使用 "na")；如果您要對已註解化的元素加入值都，請務必移除 #。
- 值 (例如標題) 中的冒號會將中繼資料剖析器中斷。 在其位置中，使用以下的 HTML 編碼&#58; (例如："title: Azure Rights Management&#58; 的基本概念 | Azure RMS")。
- **標題**︰這個標題會出現在搜尋引擎結果中。 標題結尾應該是垂直線 (|) 後面加上服務的名稱 (請參閱以上的範例)。 標題不需要 (且可能不應) 等於 H1 標題中的標題。 它應該是大約 65 個字元 (包括 | 服務名稱)
- **作者**、**管理員**、**檢閱者**︰作者欄位應包含作者的 **Github 使用者名稱**，而非其別名。  相反地，「管理員」和「檢閱者」欄位則應包含別名。 ms.reviewer 會指定與文章或服務相關聯的 PM 名稱。
- **ms.assetid**︰這是來自 CAPS 的文章的 GUID。 建立新的 Markdown 檔案時，請從 [https://www.guidgenerator.com](https://www.guidgenerator.com) 取得 GUID。 
- **ms.prod**、**ms.service**、**ms.technology**、**ms.devlang**、**ms.topic**、**ms.tgt_pltfrm**︰這些元素的可能值可以在[這裡](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default)找到。

## 基本 Markdown 和 GFM

支援所有的基本和 Github 特定 Markdown。 如需這些設定的詳細資訊，請參閱：

- [基準 Markdown 語法](https://daringfireball.net/projects/markdown/syntax)
- [Github 特定 Markdown (GFM) 文件](https://guides.github.com/features/mastering-markdown)

## 標題

以上是第一和第二個層級標題的範例。 

主題中**必須**只有一個第一層標題，它會顯示為頁面的標題。  

第二層標題將會產生頁面上的目錄，它會顯示在頁面標題的「本文內容」區段下。

### 第三個層級的標題
#### 第四個層級的標題
##### 第五個層級的標題
###### 第六個層級的標題

## 文字樣式

*斜體* 

**粗體** 

~~刪除線~~



## Links

若要連結至相同儲存機制中的 Markdown 檔案，請使用[相對連結](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)。 

- 範例：[什麼是 Azure 版權管理](./understand-explore/what-is-azure-rights-management.md)

若要連結至相同 Markdown 檔案中的標頭，請檢視已發行文章的來源、尋找標頭的識別碼 (例如 `id="blockquote"`)，並使用 # + 識別碼連結 (例如 `#blockquote`)。

- 範例︰[Blockquotes](#blockquote)

若要連結至相同儲存機制的 Markdown 檔案中的標頭，請使用相對連結 + 雜湊標記連結。

- 範例：[註冊程序的技術概觀](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

若要連結至外部檔案，請使用完整 URL 做為連結。

- 範例︰[Github](http://www.github.com)

如果 URL 出現在 Markdown 檔案中，則會將它轉換成可點按的連結。

- 範例︰http://www.github.com

## 清單

### 排序的清單

1. 這 
1. 是
1. 一個
1. 排序
1. 清單  


#### 具有內嵌清單的排序清單

1. 這裡
1. 是
1. 一個
1. 內嵌
    1. Miss Scarlett
    1. Professor Plum
1. 排序
1. 清單


### 未排序的清單

- 如果
- 是
- 一個
- 項目符號
- 清單


##### 具有內嵌清單的未排序清單

- 如果 
- 項目符號 
- 清單
    - Mrs. Peacock
    - Mr. Green
- 包含  
- 其他
    1. Colonel Mustard
    1. Mrs. White
- 清單


## 水平尺規

---

## 資料表

| 資料表        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| col 1 is default | left-aligned     |    $1 |


## 程式碼

### 程式碼區塊

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### 內嵌程式碼

這是 `in-line code` 的範例。

## Blockquotes

> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.

## 映像

### 靜態影像

![這是替代文字](./media/AzRMS_elements.png)

### 連結的影像

[![a連結影像的替代文字](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### 動畫 GIF

![動畫 GIF](./media/hololens.gif)

## 警示

### 附註

> [!NOTE] 這是備註

### 警告

> [!WARNING] 這是警告

### 提示

> [!TIP] 這是提示

### 重要

> [!IMPORTANT] 這是重要事項

## 影片

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms 副檔名
以下是可用的擴充功能︰

### 按鈕

> [!div class="button"] [按鈕連結](/rights-management)

### 選取器

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### 逐步

>[!div class="step-by-step"] [上一步](https://www.example.com)
[下一步](https://www.example.com)

<!--HONumber=May16_HO3-->


