# tcpa
优势：TCPA启用后，小文件比BBR能提升40%以上，大文件比BBR能提升5%~10%。TCPA的优势在于小文件的性能提升，程序也默认仅加速网站端口(80/443/8080)，所以更适用于建站场景。

环境要求:
centos7
/boot分区≥500M(太小会安装失败)

一、一键安装

wget http://down.08mb.com/tcp_opz/tcpa/tcpa.sh

或

wget --no-check-certificate https://raw.githubusercontent.com/wangzhe12588/tcpa/master/tcpa.sh

sh tcpa.sh

使用说明:一键包会自动安装依赖(仅epel-release、net-tools)和内核并重启，重启后安装自动完成无需人工干预。

二、手动安装：

参考：https://www.lijian.me/141.html

部署流程：

安装必要依赖:

yum -y install net-tools

更换系统内核

wget --no-check-certificate https://raw.githubusercontent.com/wangzhe12588/tcpa/master/kernel-3.10.0-693.5.2.tcpa06.tl2.x86_64.zip && wget --no-check-certificate https://raw.githubusercontent.com/wangzhe12588/tcpa/master/kernel-3.10.0-693.5.2.tcpa06.tl2.x86_64.z01

yum install -y unzip zip

cat kernel-3.10.0-693.5.2.tcpa06.tl2.x86_64.z*>kernel-3.10.0-693.5.2.zip

unzip kernel-3.10.0-693.5.2.zip

rpm -ivh kernel-3.10.0-693.5.2.tcpa06.tl2.x86_64.rpm --force



重启操作系统

reboot

下载主程序：

wget --no-check-certificate https://github.com/wangzhe12588/tcpa/raw/master/tcpa_packets_180619_1151.tar.gz

开始安装：

tar xf tcpa_packets_180619_1151.tar.gz

cd tcpa_packets

sh install.sh

TCPA(默认只加速80,443,8080这3个端口)，如需新增加速端口:

vim /usr/local/storage/tcpav2/start.sh

第46行后添加:

$BINDIR/$CTLAPP access add tip $ip tport 自定义端口

启动tcpa拥塞算法：

cd /usr/local/storage/tcpav2

sh start.sh

查看是否开启成功

[root@vultr tcpav2]# lsmod|grep tcpa

tcpa_engine           224249  0

卸载方法:

cd /usr/local/storage/tcpav2

sh uninstall.sh
