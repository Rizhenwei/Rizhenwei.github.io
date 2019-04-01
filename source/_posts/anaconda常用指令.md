---
title: Anaconda 常用指令
date: 2019-03-25 21:40:30
categories: python
tags:
series:
description: Anaconda 常用指令
keywords: 
- python
- Anaconda
---

# Anaconda 常用指令
> tip python 环境管理
[官网下载地址](https://www.anaconda.com/distribution/)

1. 查看安装的版本：  `conda --version`
2. 更新所有工具包：   `conda upgrade --all`
3. 激活默认虚拟环境：     `activate`, 默认为base环境，激活特定环境 `activate env_name`
4. 创建一个虚拟环境：  `conda create -n env_name python=3`，指定python版本为3的env_name环境
5. 安装第三方包： `conda install requests` 或 `pip install requests`
6. 卸载第三方包：`conda remove requests` 或 `pip uninstall requests`
7. 查看环境安装了那些包： `conda list`
8. 导出环境：`conda env export >env.yaml`
9. 导入环境： `conda env create -f env.yml`