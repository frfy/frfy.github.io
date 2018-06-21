---
title: Python 离线环境配置
tags:
	- Triks
---
python 离线环境配置
<!--more-->
* 导出pip 安装的list列表到requirements.txt
	
```	
pip freeze >requirements.txt
```	
	
* 将requirements.txt中依赖包按照list下载到本地
	
```	
pip download -d c:/pgk -r requirements.txt
```	
	
* 将按照requirements.txt下载到本地依赖包安装	
	
```	
pip install --no-index --find-links=c:/pgk -r requirements.txt
```	