# Aria2-AriaNg

[![](https://img.shields.io/badge/AriaNg-1.1.7-blue)](https://img.shields.io/badge/AriaNg-1.1.7-blue "AriaNg版本")
<!-- [![](https://img.shields.io/badge/Aria2-1.1.7-blue)](https://img.shields.io/badge/AriaNg-1.1.7-blue "AriaNg版本") -->

Aria2 with Aira-Ng web UI.

## Brief Introduction
* Use Apline:latest as base image, full image only **18Mb**.
* You can edit aria2 config file out of the image.
* Use Aria-Ng as aria2 web ui, it seems much more beautiful.
* Use darkhttpd as http server, it's very small(Only 36K after complied) and easy to use.

## Build
```
git clone https://github.com/mengbai0/aria2-ariang.git
cd aria2-ariang
docker build -t mengbai0/aria2-ariang .
```

## Install
1. Mount `/DOWNLOAD_DIR` to `/aria2/downloads` and `/CONFIG_DIR` to `/aria2/conf`. When starting container, it will create  `aria2.conf` file with default settings.
2. Mapping ports:
  * 6800 for aira2 service
  * 80 for Aria-Ng http service
  * 8080 for downloads directory http service
3. Set your secret code use "SECRET" variable, this will append `rpc-secret=xxx` to aira2.conf file.

Run command like below(You may need to change the ports).
```
docker run --name aria2-ariang \
-p 6800:6800 -p 6880:80 -p 6888:8080 \
-v /DOWNLOAD_DIR:/aria2/downloads \
-v /CONFIG_DIR:/aria2/conf \
-e SECRET=YOUR_SECRET_CODE mengbai0/aria2-ariang
```
After finished, open http://serverip:6880/ in your browser for visiting Aria-Ng home page, open http://serverip:6888/ to browser your downloads folder.
