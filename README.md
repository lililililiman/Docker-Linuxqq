Docker-Linuxqq

FROM debian:bookworm

# 安装依赖
RUN apt update && \
    apt install -y \
    x11-xserver-utils \
    xdg-user-dirs \ 
    xdg-utils \ 
    xkb-data \
    zutty \
    libasound2 
# 下载 QQ Linux 包
COPY QQ_3.2.17_250423_amd64_01.deb /root/
RUN  apt install -y /root/QQ*.deb

    
WORKDIR /root

ENV DISPLAY=:0

# 拷贝脚本

# COPY start-qq.sh /usr/local/bin/start-qq.sh
# RUN chmod +x /usr/local/bin/*.sh
RUN useradd -ms /bin/bash myuser
USER myuser

WORKDIR /home/myuser
CMD ["qq", "--no-sandbox"]
