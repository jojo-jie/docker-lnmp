FROM redis:latest
MAINTAINER walker "2725445401@qq.com"

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
#CMD ["redis-server","/data/redis.conf"]