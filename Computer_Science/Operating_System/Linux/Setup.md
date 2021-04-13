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