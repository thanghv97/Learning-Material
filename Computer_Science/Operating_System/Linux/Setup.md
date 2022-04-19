## DEVELOP
  + [Elastic Search](#001-elastic-search)
  + [Kibana](#002-kibana)
  + [Metric Beat](#003-metric-beat)
  + [Redis](#004-redis)
  + [Kafka](#005-kafka)
  + [Rabbit-MQ](#006-rabbit-mq)
  + [Apt](#007-apt)

# ------ APPLICATION -----------------------------------------
### 001. Elastic Search
  *Elasticsearch is a real-time, distributed storage, search, and analytics engine. It can be used for many purposes, but one context where it excels is indexing streams of semi-structured data, such as logs or decoded network packets.*
  + install
    + ubuntu 
		```
			curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.2-amd64.deb
			sudo dpkg -i elasticsearch-7.15.2-amd64.deb
        ```
		make sure Elasticsearch is up and running
		```
			curl http://127.0.0.1:9200
		```
		```
			{
				"name" : "ibcntt-Inspiron-5502",
				"cluster_name" : "elasticsearch",
				"cluster_uuid" : "Jd0SSqQ5SGOguvV6IUrpCA",
				"version" : {
					"number" : "7.15.2",
					"build_flavor" : "default",
					"build_type" : "deb",
					"build_hash" : "93d5a7f6192e8a1a12e154a2b81bf6fa7309da0c",
					"build_date" : "2021-11-04T14:04:42.515624022Z",
					"build_snapshot" : false,
					"lucene_version" : "8.9.0",
					"minimum_wire_compatibility_version" : "6.8.0",
					"minimum_index_compatibility_version" : "6.0.0-beta1"
				},
				"tagline" : "You Know, for Search"
				}
		```
  + operator 
    + start 
		```
			sudo /etc/init.d/elasticsearch start
		```
  + setting
	+ config `/etc/elasticsearch/`
	+ log `/var/log/elasticsearch/` 
  + error:
    + cannot running elasticsearch.service 
		+ check memory ram Heap Min Capacity & Heap Initial Capacity in log file enough, if lack than setting -Xms and -Xmx in config file `elasticsearch.yml`
		
			Modify the value of -Xms and -Xmx to no more than 50% of your physical RAM. The value for these settings depends on the amount of RAM available on your server. Elasticsearch requires memory for purposes other than the JVM heap and it is important to leave space for this.
			```
				-Xms2048m
				-Xms2048m
			```

### 002. Kibana
  + install
    + ubuntu 
		```
			curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-7.15.2-linux-x86_64.tar.gz
			tar xzvf kibana-7.15.2-linux-x86_64.tar.gz
			cd kibana-7.15.2-linux-x86_64/
		```
  + operators
    + start
		```
			./bin/kibana
		```
  	+ web interface `http://127.0.0.1:5601`

### 003. Metric Beat
  + install 
    + ubuntu

### 004. 


### 007.Apt
  + error
    1. Doesn't support architecture 'i386'
      + description
		```
			N: Skipping acquire of configured file 'main/binary-i386/Packages' as repository 'http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease' doesn't support architecture 'i386'
		```
	  + solution
	    + find defined file for repo
		  ``` 
		    sudo grep -i postgresql /etc/apt/sources.list
			or 
			sudo grep -i postgresql /etc/apt/sources.list.d/*.list
		  ```
		+ edit file 
		  ```
		    sudo vim /etc/apt/sources.list
			or
			sudo vim /etc/apt/sources.list.d/{found_filename}.list
		  ```
		+ change line 
		  ```
		    deb https://blah blah blah 
			to 
			deb [arch=amd64] https://blah blah blah
		  ```
	2. Cannot connection - connection time out 
	  + description

	  + solution
	    + maybe you're using a proxy 
		  ```
		    check /etc/apt/apt.conf.d/proxy.conf
			if using a proxy 
			  Acquire
				{
					HTTP::proxy ".....";
					HTTPS::proxy ".....";
				}
			change it 
			  Acquire
				{
					HTTP::proxy "false";
					HTTPS::proxy "false";
				}
		  ```

+ common
	+ vim:
	+ htop:
	+ net-tools: ifconfig
	+ openssh-server:
	+ cmake: 3.18.3
	+ vscode:
	+ git:
	+ ibus-unikey: vietnamese keyboard
	+ microsoft-teams: <for job>
    + sticky-note like window: indicator-stickynotes
+ optional:
	+ cpufrequtils: for performance ubuntu

+ Autopilot Project
	+ nvidia-driver:
		+ ubuntu-drivers devices
		+ sudo ubuntu-drivers autoinstall 
		+ sudo apt-get install <recommend driver>
	+ cuda-toolkit: 10.2
		+ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
		+ sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
		+ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
		+ sudo add-apt-repository "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /"
		+ sudo apt-get update
		+ sudo apt-get -y install cuda-10-2
	+ python3-opencv:
	+ python3-pip:
	+ numpy: pip3
	+ matplotlib: pip3
	+ scikit-image: pip3

	+ opencv_c++:
	+ eigen_c++:

	+ vtk-6:
	+ ros-melodic-desktop-full: compatible with vtk-6

+ CI/CD: Git - Jenkin
	+ Jenkin:
		+ install jdk 8 or 11
			- sudo apt-get install openjdk-8-jdk
			- sudo apt-get install openjdk-11-jdk
		+ install jenkins
			- sudo wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
			- sudo echo 'deb https://pkg.jenkins.io/debian-stable binary/' > /etc/apt/sources.list.d/jenkins.list
			- sudo apt update
			- sudo apt install jenkins -y
		+ start and enable service jenkins
			- systemctl start jenkins 
			- systemctl enable jenkins
		+ open tcp port 8080(default config port for jenkins)
			- tcp -A INPUT -p tcp --dport 8080 -j ACCEPT
		+ open web jenkin: https://localhost:8080/ with password in /var/lib/jenkins/secrets/initialAdminPassword

	- Reference:
		+ https://cuongquach.com/cai-dat-jenkins-tren-ubuntu-18-04.html