- ####  #!/bin/bash
- ####  A && B || C //若B不执行，也会执行C
---
- ####  [ -z $NB ]  [ ! -z $NB ]  //判断$NB是不是空值
- ####  PS： [ ] 不支持小数点，有小数点都返回错误
--- 
- ####  -e  //是否存在
- ####  -f  //文件
- ####  -d  //目录
- ####  -r  //读   #root是上帝，一般都为真
- ####  -w  //写   #root是上帝，一般都为真
- ####  -x  //执行 #root也不能执行没有x权限的文件
---
- ####  ping -i0.01 //每0.01秒ping一次 -c2 //ping2次  -W1 //最长等待回馈时间1s
---
- ####  ${#p} 			 //确定字符串p的长度
- ####  p=1382355031 8
- ####    0123456789 10		 //start from 0
- ####  echo ${p:1:2}  		 -->  38
- ####  #echo ${p:5:30} 		 -->  550318
- ####  #expr substr "$p" 1 1     -->  1		//start from 1
- ####  #echo $p | cut -b 1 3	 -->  138  	//start from 1
- ####  	      -b  	 //			
- ####  ${p/old/new}  		 #replace the first one
- ####  ${p//old/new}  		 #replace all
- ####  ${p#*:} 		 #delete left of first ':'(include ':')
- ####  ${p##*:}		 #delete left of last  ':'(include ':')
- ####  ${p%:*}			 #delete right of first ':'(include ':')
- ####  ${p%%:*}		 #delete right of last  ':'(include ':')
- ####  ${p:-123} 		 #如果p为空，则输出123
- ####  x=(11 22 33 44)      	 #数组
- ####  x[0]=11
- ####  x[1]=22 		 #一次添加一个数
- ####  echo ${x[0]}	 	 #取数组第一个数
- ####  echo ${#x[*]} 		 #统计个数
- ####  ssh -O StrictHostKeyChecking=no   #不检查yes no
---
- ####  md5sum $1			 #查看文件$1的md5sum值
- ####  openssl genrsa > cert.key	 #生成私钥
- ####  openssl req -new -x509(证书的类型) -key cert.key > cert.pem #生成证书（公钥）
---
- ####  LNMP (linux,Nginx(80),Mysql(3306),Php(9000))
- ####  mariadb-server mariadb-devel 
- ####  php php-fpm php-mysql (systemctl enable php-fpm)
- ####  常见错误
- ####  1.没有test.php			#/usr/local/nginx/logs/error.log
- ####  	File not found
- ####  2.nginx || php 没有启动
- ####  	无法连接
- ####  	An error
- ####  3.test.php 脚本有错误		#/var/log/php-fpm/www-error.log
- ####  	空白
- ####  4.动静分离没有做好		
- ####  	下载文件
---
- ####  --with-stream
- ####  --with-http_stub_status_module
- ####  --with-http_ssl_module
- ####  
- ####  在服务器添加完公钥后报错
- ####  sign_and_send_pubkey: signing failed: agent refused operation
- ####  这个时候我们只要执行下
- ####  eval "$(ssh-agent -s)"
- ####  ssh-add
- ####  就可以了
---
