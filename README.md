---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Adobe Commerce Intelligence技术文档

我们欢迎社区以及文档团队以外的Adobe员工投稿。

## Adobe Open Source行为准则

本项目已采用 [Adobe 开源行为准则](code-of-conduct.md)或 [.NET Foundation 行为准则](https://dotnetfoundation.org/code-of-conduct)。有关更多信息，请参阅[贡献](contributing.md)文章。

## 关于您对Adobe内容的投稿

请参阅[Adobe文档参与者指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hans)。

您的参与方式取决于您的身份以及您想参与的更改类型：

### 次要更改

如果您要提供较小的更新，请访问文章，然后单击文章底部显示的反馈区域，单击&#x200B;**详细的反馈选项**，然后单击&#x200B;**建议编辑**&#x200B;以转到GitHub上的Markdown源文件。 使用GitHub UI进行更新。 有关详细信息，请参阅常规的[Adobe Docs参与者指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hans)。

您为此存储库中的文档和代码示例提交的小幅度更正或说明受Adobe使用条款的约束。

### 社区成员的重大更改或新文章

如果您是Adobe社区的一员，并且希望创建新文章或提交重大更改，请使用Git存储库中的“问题”选项卡来提交问题，从而开始与文档团队的对话。 一旦您同意了计划，您将需要与员工合作，通过公共和专用存储库中的工作组合来帮助引入新内容。

### Adobe员工做出的主要更改

如果您是来自Adobe Experience Cloud解决方案产品团队的技术文档撰稿人、项目经理或开发人员，并且您的工作就是撰写或创作技术文章，那么您应当使用位于`https://git.corp.adobe.com/AdobeDocs`的专用存储库。

## 工具和设置

社区参与者可以使用GitHub UI进行基本编辑或创建存储库分支以进行重大更改。

有关详细信息，请参阅[Adobe Docs参与者指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hans)。

## 如何使用Markdown格式化主题

此存储库中的所有文章都使用GitHub风格的标记。 如果您不熟悉Markdown，请参阅：

- [标记基础知识](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [可打印的Markdown速查表](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## 用于图像优化的预提交挂接

此存储库包括自动预提交挂接，用于在提交之前优化图像。 **所有参与者都应启用这些挂接**，以确保一致的图像优化并降低存储库大小。

### 快速设置

克隆存储库后，运行：

```bash
.githooks/setup-hooks.sh
```

### 钩子做什么

- 自动检测暂存的图像文件(PNG、JPG、JPEG、GIF、SVG)
- 运行`image_optim`以压缩和优化图像
- 自动重新存放优化的图像
- 确保所有提交的映像都得到了正确优化

### 优点

- 减少了存储库大小
- 更快地加载文档的页面
- 所有参与者均具有一致的图像质量
- 无需手动优化

有关详细的设置说明、疑难解答和配置，请参阅[`.githooks/README.md`](.githooks/README.md)。
