### swift in docker 


容器内运行swift ：  

	docker pull serverascode/swift-onlyone
	docker run --rm -v /srv:/srv -p 8080:8080 serverascode/swift-onlyone 
	
	docker run -i -t serverascode/swift-onlyone /bin/bash
	/usr/local/bin/startmain.sh 
	
	#暴露外部访问http接口
	docker run -d -p 8080:8080 -t serverascode/swift-onlyone
	
	#api控制
	swift -A http://127.0.0.1:8080/auth/v1.0 -U test:tester -K eimuigaafooc stat
	swift -A http://127.0.0.1:8080/auth/v1.0 -U test:tester -K eusaneinoovo upload etc_swift /etc/swift
	
	serverascode/swift-onlyone镜像的auth账号是  test:tester 密码在  proxy_server.conf的 tempauth中定义，密码随机
	

####swift 访问存取

	
’‘’
	
	--------------------
	#用户登陆
	curl -v -H 'X-Auth-User: test:tester' -H 'X-Auth-Key: xeepadumarah' http://centos66:8080/auth/v1.0
	#验证登陆
	curl -v -H 'X-Auth-Token: AUTH_tkd9126367e53f41a5b59740227859102a'  http://centos66:8080/v1/AUTH_test

	#创建container
	curl -v -X PUT -H 'X-Storage-Token: AUTH_tkd9126367e53f41a5b59740227859102a'  http://centos66:8080/v1/AUTH_test/folder1
	#上传文件
	curl  -X PUT -H 'X-Storage-Token: AUTH_tkd9126367e53f41a5b59740227859102a'  http://centos66:8080/v1/AUTH_test/folder1/ -T ./gou.jpg
	#获取文件 
	curl  -X GET -H 'X-Storage-Token: AUTH_tkd9126367e53f41a5b59740227859102a'  http://centos66:8080/v1/AUTH_test/folder1/gou.jpg -o aaa.jpg
	
	-o：将文件保存为命令行中指定的文件名的文件中
	-O：使用URL中默认的文件名保存文件到本地
	--------------------
	
	
	swift -A http://127.0.0.1:8080/auth/v1.0 -U test:tester -K testing stat
	swift -A http://127.0.0.1:8080/auth/v1.0 -U test:tester -K testing stat
	
	
	curl  -X GET -H 'X-Auth-Token: AUTH_tk1e655df567724453a7343c6b6359e327'  http://localhost:8080/v1/AUTH_test/folder1?format=json
	
	curl -v -X PUT -H 'X-Storage-Token: AUTH_tk1e655df567724453a7343c6b6359e327'  http://localhost:8080/v1/AUTH_test/folder1
	
	登录
	curl -v -H 'X-Auth-User: test:tester' -H 'X-Auth-Key: agahbereisee' http://localhost:8080/auth/v1.0
	curl -v -H 'X-Storage-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c'  http://localhost:8080/v1/AUTH_test
	
	创建container
	curl -v -X PUT -H 'X-Storage-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c'  http://localhost:8080/v1/AUTH_test/folder1
	
	获取制定资源的相关信息 json格式返回 
	curl  -X GET -H 'X-Auth-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c'  http://localhost:8080/v1/AUTH_test/folder1?format=json
	
	
	
	curl -v -H 'X-Auth-User: test:tester' -H 'X-Auth-Key: eimuigaafooc' http://centos66:8080/auth/v1.0
	curl  -X PUT -H 'X-Auth-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c'  http://centos66:8080/v1/AUTH_test/folder1/ -T ./gou.jpg
	
	

	< X-Storage-Url: http://localhost:8080/v1/AUTH_test
	< X-Auth-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c
	< Content-Type: text/html; charset=UTF-8
	< X-Storage-Token: AUTH_tk924fe7ba93cc45fcb3b4e778ba94203c
	< Content-Length: 0
	< X-Trans-Id: tx6f0f114e93024eb6b27dc-0055e28079

‘’‘

### install swift 


	rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
	yum install git curl gcc memcached rsync sqlite xfsprogs git-core \                       libffi-devel xinetd python-setuptools python-coverage \                       python-devel python-nose python-simplejson pyxattr \                       python-eventlet python-greenlet python-paste-deploy \                       python-netifaces python-pip python-dns python-mock -y
	pip install pyeclib 
	pip install -U xattr    pip install eventlet
    pip install -r swift/requirements.txt    
	
	
#####安装swift
	mkdir -p /opt
	cd /opt    git clone https://github.com/openstack/python-swiftclient.git    cd /opt/python-swiftclient; 
	python setup.py install;    
    pip install -r requirements.txt;    
    cd /opt    r access to an upst    cd /opt/swift ;     python setup.py install;	
	
	dd if=/dev/zero of=disk1 bs=1M count=1024 
	mkfs.xfs -f -i size=1024 ./disk	1
	mkdir -p /srv/node/sdb1
	mount -t xfs -o loop ./disk1 /srv/node/sdb1


	mkdir -p /etc/swift    cd /opt/swift/etc    cp account-server.conf-sample /etc/swift/account-server.conf    cp container-server.conf-sample /etc/swift/container-server.conf    cp object-server.conf-sample /etc/swift/object-server.conf    cp proxy-server.conf-sample /etc/swift/proxy-server.conf    cp drive-audit.conf-sample /etc/swift/drive-audit.conf    cp swift.conf-sample /etc/swift/swift.conf


###创建builder-files

'''

	cd /etc/swift
    swift-ring-builder account.builder create 18 3 1
    swift-ring-builder container.builder create 18 3 1
    swift-ring-builder object.builder create 18 3 1
    
    swift-ring-builder object-1.builder create 17 4 1
    swift-ring-builder object-2.builder create 17 3 1

    swift-ring-builder account.builder add r1z1-127.0.0.1:6002/sdb1 100
    swift-ring-builder container.builder add r1z1-127.0.0.1:6001/sdb1 100
    swift-ring-builder object.builder add r1z1-127.0.0.1:6000/sdb1 100
    
    swift-ring-builder object-1.builder add r1z1-127.0.0.1:6000/sdb1 100
    swift-ring-builder object-2.builder add r1z1-127.0.0.1:6000/sdb1 100

    swift-ring-builder account.builder add r1z1-127.0.0.1:6002/d2 100
    swift-ring-builder container.builder add r1z1-127.0.0.1:6001/d2 100
    swift-ring-builder object.builder add r1z1-127.0.0.1:6000/d2 100
    swift-ring-builder object-1.builder add r1z1-127.0.0.1:6000/d2 100
    swift-ring-builder object-2.builder add r1z1-127.0.0.1:6000/d2 100


'''

###build ring-files

'''

	cd /etc/swift    swift-ring-builder account.builder rebalance    swift-ring-builder container.builder rebalance    swift-ring-builder object.builder rebalance
        swift-ring-builder object-1.builder rebalance    swift-ring-builder object-2.builder rebalance	生成ring文件: 
	account.ring.gz 	container.ring.gz
	object.ring.gz	object-1.ring.gz
	object-2.ring.gz'''


##Configuring Proxy Server

'''
	
	head -c 32 /dev/random | base64
	
	
	[swift-hash]
	swift_hash_path_suffix = RzUfDdu32L7J2ZBDYgsD6YI3Xie7hTVO8/oaQbpTbI8=
	swift_hash_path_prefix = OZ1uQJNjJzTuFaM8X3v%fsJ1iR#F8wJjf9uhRiABevQ4
'''   
	swift-init proxy-server start
	swift-init account-server start 
	swift-init container-server start 
		
###TempAuth Authentication and Authorization
启动memcached
	service memcached start	chkconfig memcached on
