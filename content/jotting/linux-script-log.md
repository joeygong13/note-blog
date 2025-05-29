+++
date = '2025-05-29T19:50:28+08:00'
draft = false
title = 'Linux Script 输出日志'
description = '在 Linux 脚本中输出日志'
categories = ['随笔']
tags = ['syslog']
+++


当我们执行脚本时，特别时执行定时任务脚本时，我们想保存日志，可以利用现成的 logger

在执行脚本 `script.sh` 时，添加管道  `logger -t custom_tag`，如

```bash
sh script.sh | logger -t custom_tag

# 随后即可通过标签 custom_tag 进行日志搜索
grep 'custom_tag' /var/log/syslog
```
