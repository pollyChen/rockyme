title: Fastdfs 图片压缩
desc: Fastdfs nginx lua GraphicsMagick 图片压缩。最近项目的访问量急剧上升，带宽也急剧上升，由于图片访问量太大导致。
category: FastDFS
date: 2015.08.13
---

由于网站的访问量在稳步上升，而网站最大的流量是图片。故做此记录，做备忘。

### 安装nginx + lua ###
这里我选择使用[OpenResty](http://openresty.org/)，其中，包含有Nginx核心和其它第三方模块。OpenResty最大的亮点在于默认集成Lua开发环境。

安装步骤如下：
1. 新建安装目录（个人喜好），将所有相关软件都在此目录安装，后续统一管理。
``` shell
    mkdir -p /usr/local/nginx-lua-space/
    cd /usr/local/nginx-lua-space/
```
