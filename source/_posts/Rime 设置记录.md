---
title: Rime 设置记录
top: false
cover: false
toc: true
date: 2024-05-03 23:12:25
password:
math:
mermaid:
summary:
tags:
    - 记录
    - 输入法
categories: 技术
---

## 前言
Rime 是一个开源的跨平台输入法。但每次安装都要重新设置一番，而设置方法又常常忘记，因此记录一下。

## 配置
配置文件在用户文件夹，修改 `default.custom.yaml` 文件即可。

```yaml
patch:
  menu:
    page_size: 9    # 每页九个候选
  ascii_composer:
    switch_key:
      Shift_L: commit_code  # 左shift键自动上屏并切换成英文
      Enter: inline_ascii   # 回车键自动上屏
```

## 日语输入
使用[Rime-Japanese](https://github.com/gkovacs/rime-japanese)给出的方案。直接从输入法设定中输入网址安装即可。如果无法连接网络，手动下载安装[東風破Plum](https://github.com/rime/plum)。反正很小，放在一起也无妨。