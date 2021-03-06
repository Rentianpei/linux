- ## GRE    
    - ### 步骤
        - ##### 通过命令<==modprobe ip_gre==>启动模块
        - ##### 通过命令<ip tunnel add “隧道名” mode “模式” remote “对方ip” local “我方ip”>建立隧道
            - ip tunnel add tun0  mode gre remote 201.1.2.5 local 201.1.2.10
            - ip tunnel add创建隧道（隧道名称为tun0），ip tunnel help可以查看帮助
            - mode设置隧道使用gre模式
            - local后面跟本机的IP地址，remote后面是与其他主机建立隧道的对方IP地址
            - 可以通过< ip link >查看

        -  ##### 通过命令<ip link set “隧道名” up> 启动隧道
        - ##### 通过命令<ip addr add *.*.*.*/24 peer *.*.*.*/24 dev “隧道名”>为隧道设置ip
            - ip addr add 10.10.10.10/24 peer 10.10.10.5/24 dev tun0
            - 为隧道tun0设置本地IP地址（10.10.10.10.10/24）
            - 隧道对面的主机IP的隧道IP为10.10.10.5/24
            - 通过< ip a s >查看
        - #### 在另一台主机作同样的配置，但是ip应该是镜像关系
---
- ## PPTP
    - ### 软件包 < pptpd >
    - ### 配置
        -  ##### 路径： <==/etc/pptpd.conf==> <==/etc/ppp/options.pptpd==> <==/etc/ppp/chap-secrets==>
        - ##### 文件：     <[pptpd.conf](https://github.com/guiaiy/linux/blob/master/VPN/pptpd.conf)>         <[options.pptpd](https://github.com/guiaiy/linux/blob/master/VPN/options.pptpd)>             <[chap-secrets](https://github.com/guiaiy/linux/blob/master/VPN/chap-secrets)>
        - ##### 运行命令< echo "1" > /proc/sys/net/ipv4/ip_forward >开启路由转发(临时)
        - ##### 运行命令< echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf > 开启路由转发(永久)
        - ##### 运行命令< iptables -t nat -A POSTROUTING -s 192.168.3.0/24 -j SNAT --to-source 201.1.2.5>使用NAT技术将私网ip转换
---
- ## Lt2p&IPSec
    - ### 软件包 < libreswan > < xl2tpd >
    - ### 配置
        - ##### libreswan路径： <==/etc/ipsec.d/myipsec.conf==> <==/etc/ipsec.d/mypass.secret==>
        - ##### libreswan文件： <[myipsec.conf](https://github.com/guiaiy/linux/blob/master/VPN/myipsec.conf)>                   <[mypass.secret](https://github.com/guiaiy/linux/blob/master/VPN/mypass.secrets)>
        - ###### libreswan 进程名：<==pluto==>
        - ##### xl2tpd路径： <==/etc/xl2tpd/xl2tpd.conf==> <==/etc/ppp/options.xl2tpd==> <==/etc/ppp/chap-secrets==>
        - ##### xl2tpd文件：       <[xl2tpd.conf](https://github.com/guiaiy/linux/blob/master/VPN/xl2tpd.conf)>                       <[options.xl2tpd](https://github.com/guiaiy/linux/blob/master/VPN/options.xl2tpd)>              <[chap-secrets](https://github.com/guiaiy/linux/blob/master/VPN/chap-secrets)>
---
