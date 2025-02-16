---
☀️日期☀️: "{{date}}"
📆星期📆: <% tp.file.creation_date("dddd") %>
⌚️时间⌚️: "{{time}}"
🌍位置🌍: 【功能制作中！计划使用GPS位置信息录入】
cssclasses:
  - hide-metadata
create_device: 
uid:
  - uid_<% Date.now() %>
aliases:
---

> 这篇日记使用**quick add命令**来操作 [[#计划]] [[#流水帐]] 以及 [[#闪念 Memos Zone]] 模块。**如无必要请勿手动调整。**
## 日程 Plan & Review

### 计划

| 时间段 | 要干的事 |
| ---- | ---- |
| 00:00-{{time:HH:mm}} |  |
|  |  |
| -24:00 |  |

### 流水帐




## 闪念 Memos Zone

## 正文 Daily Note

<% tp.file.cursor() %> <%* app.workspace.activeLeaf.view.editor?.focus(); %>