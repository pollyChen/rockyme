title: Fastdfs 图片压缩
desc: Fastdfs nginx lua GraphicsMagick 图片压缩。最近项目的访问量急剧上升，带宽也急剧上升，由于图片访问量太大导致。
category: FastDFS
date: 2015.08.13
---

由于网站的访问量在稳步上升，而网站最大的流量是图片。

### 安装nginx + lua ###
这里我选择使用[OpenResty](http://openresty.org/)，其包含有Nginx核心和其它第三方模块。OpenResty最大的亮点在于默认集成Lua开发环境。

安装步骤如下：
1. ####新建安装目录（个人喜好）####  
  将所有相关软件都在此目录安装，后续统一管理。
``` vim  
mkdir -p /usr/local/nginx-lua-space/      
cd /usr/local/nginx-lua-space/  
```


2. ####安装依赖环境####  
    如果在安装fastdfs时，已经安装过，请忽略此步。
    备注：这里使用的系统为centos6.5。
``` vim
yum install libreadline-dev libncurses5-dev libpcre3-dev libssl-dev perl
```


3. ####下载最新的版本的ngxopenresty-1.9.3.1.tar.gz并解压####
``` vim
wget https://openresty.org/download/ngxopenresty-1.9.3.1.tar.gz
tar -zvxf ngxopenresty-1.9.3.1.tar.gz
```

4. ####安装LuaJIT####
``` vim
cd ngxopenresty-1.9.3.1/bundle/LuaJIT-2.1-20150120/
make clean && make && make install
```

5. ####下载ngxcachepurge模块，该模块用于清理nginx缓存####
``` vim
cd ..
wget https://github.com/FRiCKLE/ngxcachepurge/archive/2.3.tar.gz
tar -zxvf 2.3.tar.gz
```

6. ####下载nginxupstreamcheckmodule模块，该模块用于upstream健康检查####
``` vim
wget https://github.com/yaoweibin/nginxupstreamcheckmodule/archive/v0.3.0.tar.gz 
tar -zxvf v0.3.0.tar.gz
```
7. ####下载fastdfs-nginx-module模块，该模块用于fastdfs http下载####
``` vim
wget http://sourceforge.net/projects/fastdfs/files/FastDFS%20Nginx%20Module%20Source%20Code/fastdfs-nginx-modulev1.15.tar.gz/download
tar -zxvf fastdfs-nginx-modulev1.15.tar.gz
```

8. ####安装nginx####
``` vim
cd ..
./configure --prefix=/usr/local/nginx-lua-space --with-httprealipmodule  --with-pcre  --with-luajit --add-module=./bundle/ngxcachepurge-2.3/ --add-module=./bundle/fastdfs-nginx-modulev1.15/ --add-module=./bundle/nginxupstreamcheckmodule-0.3.0/ -j2
make && make install
```

9. ####检查nginx是否安装完成####
``` vim
cd ..
./nginx/sbin/nginx -V
```
    如果出现安装时所添加的参数，即安装成功。
    
    
###GraphicsMagick###
相信做过互联网图片的人都知道ImageMagick，超牛逼的图片处理库，而GraphicsMagick是从ImageMagick5.5.2的分支版本，支持多达88种图片格式的处理，而且相当稳定及高效。

``` vim
wget ftp://ftp.graphicsmagick.org/pub/GraphicsMagick/1.3/GraphicsMagick-1.3.1.tar.gz
tar -zvxf GraphicsMagick-1.3.1.tar.gz
./configure --prefix=/usr/local/graphicsmagick-1.3.17
make && make install
```
###fastdfs nginx lua GraphicsMagick 整合###
此整合模块已经有人完全写好，本人将其fork到本地。具体内容请参考我的[<i class="fa fa-github"></i>](https://github.com/tryndamere/nginx-lua-fastdfs-GraphicsMagick)


###参考网址###
*  http://jinnianshilongnian.iteye.com/blog/2186270
*  http://www.nongzusa.com/blog/2013/12/09/fastdfs-plus-nginx-plus-lua-plus-graphicsmagickshi-shi-suo-lue-tu/


