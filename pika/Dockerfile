FROM centos:latest
MAINTAINER cuixin <steven.cuixin@gmail.com>

RUN rpm -ivh https://mirrors.ustc.edu.cn/epel/epel-release-latest-7.noarch.rpm && \
    yum -y update && \
    yum -y install snappy-devel && \
    yum -y install protobuf-devel && \
    yum -y install gflags-devel && \
    yum -y install glog-devel && \
    yum -y install gcc-c++ && \
    yum -y install make && \
    yum -y install git && \
    rm -rf /var/cache/yum && \
    git clone https://github.com/Qihoo360/pika.git && \
    cd pika && \
    make && \
    cp output/bin/pika /bin && \
    cp output/conf/pika.conf /etc && \
    cd ../ && rm -rf pika && \
    mkdir -p /data/log && \ 
    mkdir -p /data/db && \
    mkdir -p /data/dump && \
    mkdir -p /data/dbsync && \
    sed -i 's/\.\/log\//\/data\/log/g' /etc/pika.conf && \
    sed -i 's/\.\/db\//\/data\/db/g' /etc/pika.conf && \
    sed -i 's/\.\/dump\//\/data\/dump/g' /etc/pika.conf && \
    sed -i 's/\.\/dbsync\//\/data\/dbsync/g' /etc/pika.conf && \
    sed -i 's/\.\/pika.pid/\/data\/pika.pid/g' /etc/pika.conf

EXPOSE 9221
VOLUME ["/data/"]
CMD ["/bin/pika", "-c", "/etc/pika.conf"]