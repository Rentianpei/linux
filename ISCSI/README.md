- ### 服务端
  - #### 软件包 < targetcli >
  - #### 端口 < 3260 >
  - #### 步骤
    - #### 分区
      - ##### parted /dev/vdb mklabel gpt
      - ##### parted /dev/vdb mkpart primary 1 100%
     - #### 运行命令 < targetcli > 进行配置
       - ##### backstores/block create store /dev/vdb1
       - ##### iscsi/ create iqn.2018-11.cn.tedu:server1
        - ##### iscsi/iqn.2018-11.cn.tedu:server1/tpg1/acls create iqn.2018-11.cn.tedu:client1
         - ##### iscsi/iqn.2018-11.cn.tedu:server1/tpg1/luns create /backstores/block/store
         - ##### exit
---
- ### 客户端
   - #### 软件包 < iscsi-initiator-utils.i686 >
   - #### 步骤
     - ##### 修改配置文件
        - ##### 路径 <==/etc/iscsi/initiator.iscsi==>
        - ##### 文件 <[initiator.iscsi](https://github.com/guiaiy/linux/blob/master/ISCSI/initiatorname.iscsi)>
     - ##### < systemctl restart iscsid >
     - ##### 运行< man iscsiadm >查看发现存储的命令并执行
     - ##### 分区挂载
- ### 多路径
    - #### 软件包 < device-mapper-multipath >
    - #### 配置
      - ##### 通过命令 < /usr/lib/udev/scsi_id --whitelisted --device=/dev/sdb >获取wwid，两个磁盘应该相同
      - ##### 路径 <==/usr/share/doc/device-mapper-multipath-0.4.9/multipath.conf==>需要拷贝到/etc下
          - ##### cp /usr/share/doc/device-mapper-multipath-0.4.9/multipath.conf /etc/
      - ##### 文件 < [multipath.conf](https://github.com/guiaiy/linux/blob/master/ISCSI/multipath.conf)>
          - #### 首先卸载其他挂载，再启动服务，然后挂载