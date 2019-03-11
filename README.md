1.环境准备：
---
    ###修改用户最大可创建线程数
    [root@elk ~]# cp /etc/security/limits.d/20-nproc.conf /etc/security/limits.d/20-nproc.conf.bak
    [root@elk ~]# vi /etc/security/limits.d/20-nproc.conf
    #至少为2048
    * soft nproc 2048

    ###修改虚拟内存
    [root@elk ~]# vi /etc/sysctl.conf
    vm.max_map_count=655360
    [root@elk ~]# sysctl -p

    ###修改用户最大可创建文件数
    [root@elk ~]# cp /etc/security/limits.conf /etc/security/limits.conf.bak
    [root@elk ~]# vi /etc/security/limits.conf
    * soft nofile 65536
    * hard nofile 131072
    * soft nproc 2048
    * hard nproc 4096

2.部署ELK
---
      ###拉镜像
      [root@elk ~]# sudo docker pull sebp/elk:660

      ###启动容器
      [root@elk ~]# sudo docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk:660
