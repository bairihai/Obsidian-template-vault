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
tags:
  - ✒️原创文章
---
<% tp.file.cursor() %> <%* app.workspace.activeLeaf.view.editor?.focus(); %>