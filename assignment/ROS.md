##配置Robot operation system实验报告##

###Description
Robot operation system（ROS）是一个开放的标准平台，它提供了一系列的软件框架和工具以帮助软件开发者创建机器人应用软件。目前由OSRF负责建设和维护。

###How to install 
添加源
>     $	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'  


添加钥匙 
>     $	sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Ros/1.jpg">

更新并安装桌面版
>     $	sudo apt-get update  
>     $	sudo apt-get install ros-indigo-desktop-full
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Ros/3.jpg">

初始化环境 
>     $	sudo rosdep init 
>     $	rosdep update
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Ros/4.jpg">

设置环境
>     $	echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
>     $	source ~/.bashrc
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Ros/5.jpg">

改变终端下的环境变量并安装rosinstall命令工具
>     $	source /opt/ros/indigo/setup.bash
>     $	 sudo apt-get install python-rosinstall
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Ros/6.jpg">

###Experimental experience
ROS的安装过程实际上遇到了许多奇奇怪怪的问题，但是都在别人的帮助下安装完成了。但是还没有研究透彻怎么样用ROS来运行一个实例进行测试，希望下一次能做好充足的准备。