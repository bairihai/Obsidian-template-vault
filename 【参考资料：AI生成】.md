---
☀️日期☀️: 2025-08-28
⌚️时间⌚️: 23:07
source_type: 🤖AI
source_author: gemini
source_link: （原始文章的链接）
cssclasses: 
uid:
  - uid_1756393639659
aliases: 
tags:
  - 【非原创文章】/AI生成
---
<div style="display: flex; align-items: center; text-align: center; margin: 2em 0;">
  <span style="flex-grow: 1; border-bottom: 1px solid #ccc;"></span>
  <span style="padding: 0 10px; color: #888;">以下为AI生成</span>
  <span style="flex-grow: 1; border-bottom: 1px solid #ccc;"></span>
</div>

 

> [!summary] 个人归纳
> 








看看这个obsidian的代码！/* === 段落-首行缩进2个字符 By Linzeal 2024/2/1更新 === */

/* 也包括段落中每个回车换行后的首行缩进 */

:is(
.markdown-source-view .cm-line:not(:is(:has(>.cm-hmd-frontmatter,>br),.HyperMD-header,.HyperMD-list-line,.HyperMD-quote,table .cm-line)), /* 编辑模式 */
.markdown-rendered :not(:is(blockquote)) > p /* 阅读模式 text-indent不支持each-line的办法 */
){
  text-indent: 2em !important;
}

.markdown-rendered :not(:is(blockquote)) > p
{
  /*text-indent: 2em each-line !important; 若支持each-line参数则用这个即可，更为简单，就无需下面的修正 */
}

/* 阅读模式下对每个回车换行后的首行缩进的修正 */
.markdown-rendered :not(:is(blockquote)) > p > br
{
  content:'';
  white-space:pre; 
}
.markdown-rendered :not(:is(blockquote)) > p > br::after
{
  content:'\000A\0009\00A0\00A0'; /* Unicode字符编码\0009表示水平制表符，\00A0表示不换行空格，可通过增减、组合搭配这两个Unicode字符来微调回车换行后的首行缩进量 */
}

/* === CSS代码结束 === */  这个css存在一个如图所示的问题：	callout块中图片错误触发本不能由任何图片触发的首行缩进。 如何修复？你要什么classname的话就跟我说







好的，我理解了你的问题。

你提供的这段 CSS 代码非常巧妙，旨在为 Obsidian 中的段落（包括软回车换行）添加首行缩进。问题的根源在于，目前的 CSS 选择器规则不够具体，它将所有不在块引用 (`blockquote`) 中的段落 (`<p>`) 都进行了缩进，这其中就包括了 callout 中用来包裹图片的段落。

当一个 `<p>` 标签内只包含图片时，`text-indent` 属性会导致图片有一个不必要的的水平偏移，看起来就像是错误的缩进。

### 问题修复

为了修复这个问题，我们需要修改 CSS 选择器，**让它排除掉那些包含图片的段落**。我们可以使用 `:has()` 这个 CSS 伪类选择器来实现这个功能，它能判断一个元素内是否包含另一个指定的元素。

以下是修复后的完整代码。你只需要用这段代码替换掉你原来的那段 CSS 即可。

CSS

```
/* === 段落-首行缩进2个字符 By Linzeal (Gemini 修复版) 2024/2/1更新 === */

/* 也包括段落中每个回车换行后的首行缩进 */

:is(
.markdown-source-view .cm-line:not(:is(:has(>.cm-hmd-frontmatter,>br),.HyperMD-header,.HyperMD-list-line,.HyperMD-quote,table .cm-line)), /* 编辑模式 */
.markdown-rendered :not(:is(blockquote)) > p:not(:has(img, .internal-embed, video)) /* 阅读模式：排除包含图片、内部嵌入或视频的段落 */
){
  text-indent: 2em !important;
}

.markdown-rendered :not(:is(blockquote)) > p
{
  /*text-indent: 2em each-line !important; 若支持each-line参数则用这个即可，更为简单，就无需下面的修正 */
}

/* 阅读模式下对每个回车换行后的首行缩进的修正 */
.markdown-rendered :not(:is(blockquote)) > p:not(:has(img, .internal-embed, video)) > br
{
  content:'';
  white-space:pre; 
}
.markdown-rendered :not(:is(blockquote)) > p:not(:has(img, .internal-embed, video)) > br::after
{
  content:'\000A\0009\00A0\00A0'; /* Unicode字符编码\0009表示水平制表符，\00A0表示不换行空格，可通过增减、组合搭配这两个Unicode字符来微调回车换行后的首行缩进量 */
}

/* === CSS代码结束 === */
```

### 修复说明

主要的改动有两处：

1. 我将原来的选择器 .markdown-rendered :not(:is(blockquote)) > p
    
    修改为了：
    
    .markdown-rendered :not(:is(blockquote)) > p:not(:has(img, .internal-embed, video))
    
    - **:not(:has(img, .internal-embed, video))** 这部分的意思是：选择那些 **不包含** `<img>` (图片)、`.internal-embed` (Obsidian 的内部嵌入文件) 或 `<video>` (视频) 元素的 `<p>` 段落。这样一来，任何包裹着媒体文件的段落都不会被应用首行缩进规则。
        
2. 同样地，我也将处理软回车的选择器 .markdown-rendered :not(:is(blockquote)) > p > br
    
    修改为了：
    
    .markdown-rendered :not(:is(blockquote)) > p:not(:has(img, .internal-embed, video)) > br
    
    - 这确保了针对软回车的缩进修正，也同样不会作用于包含媒体文件的段落。
        

这个修复方案应该能精确地解决你在 callout 中遇到的图片缩进问题，同时不会影响 callout 中纯文本段落的正常缩进。如果问题仍然存在，请告诉我，你可能需要使用 Obsidian 的开发者工具 (Ctrl+Shift+I) 来查看图片所在容器的具体 `classname`。