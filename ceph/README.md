  - #### 环境
    - #### 三台统一网段的主机，每个主机额外添加三块磁盘
    - #### yum源支持
    - #### 时间同步
  - #### 步骤
    - #### 三台机器根据主机名更改文件 < /etc/hosts >(案例为node1 node2 node3)
    - #### 主配置机器安装 < ceph-deploy.noarch >
    - #### 主配置机器生成密钥，实现无密码连接（包括自己）
    - #### 主配置机器生成配置目录，并cd进去（案例为ceph-cluster）
    - #### 主配置机器运行 < ceph-deploy new node1 node2 node3 >
    - #### 主配置机器运行 < ceph-deploy install node1 node2 node3 >
    - #### 主配置机器运行 < ceph-deploy mon create-initial >
    - #### 因为需要做缓存，需要将<==/dev/vdb==>分成2个区，分别做<==/dev/vdc==>和<==/dev/vdd==>的缓存
    - #### 为分/vdb2 >
    - #### 运行 < ceph-deploy osd create node1:vdc:/dev/vdb1 node1:vdc:/dev/vdb2 >为node1创建osd
    - #### 其他两台做同样的操作
    - #### ceph -s 确认状态，OK为完成状态
    - #### 运行 < rbd create demo-image(镜像名) --image-feature  layering --size 10G >
    - #### 或者 < rbd create rbd/image（镜像名） --image-feature layering --size 10 G > 创建镜像
    - #### 通过 < rbd resize > 调整镜像大小
    - #### 运行 < rbd map image > 发现镜像，需要软件包 < ceph-common >
    - #### 运行 < rbd snap create image(镜像名) --snap image-snap1(快照名) > 创建快照
    - #### 运行 < rbd snap protect image --snap image-snap1 > 禁止任何人删除快照
    - #### 运行 < rbd snap unprotect image-snap1 > 取消保护
    - #### 运行 < rbd clone image --snap image-snap1(父快照名) image-clone(子快照名) --image-feature layering > 创建克隆快照
    - #### 运行 < rbd flatten image-clone > 取消父子关系
    - #### 运行 < rbd snap rm image --snap image-snap > 删除快照