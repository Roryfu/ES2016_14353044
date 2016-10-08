##Distributed Operation Layer##

###Description
Distributed Operation Layer(DOL)是一种用于编码分布式操作的应用框架，DOL可以自动地将应用映射到多和处理器的平台上，DOL共包含以下三个基本组成成分：

- **DOL Application Programming Interface**
- **DOL Functional Simulation**
- **DOL Mapping Optimization**

###How to install 
安装一些必要的环境
>     $	sudo apt-get update  
>     $	sudo apt-get install ant  
>     $   sudo apt-get install openjdk-7-jdk  
>     $	sudo apt-get install unzip

下载一些必要的文件
>     
>     sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz  
>     sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

解压文件
> #     
>     $	mkdir dol  
>     $	unzip dol_ethz.zip -d dol  
>     $	tar -zxvf systemc-2.3.1.tgz

编译systemc 
>     $	cd systemc-2.3.1  
>     $	mkdir objdir  
>     $	cd objdir  
>     $	../configure CXX=g++ --disable-async-updates
>     $   sudo make install

编译dol
> 进入dol文件夹，修改build_zip.xml文件
```<property name="systemc.inc" value="YYY/include"/> ``` 
```<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>```
> 编译文件  
```$	ant -f build_zip.xml all```

###Experimental experience
第一次使用markdown来编辑实验文档，感觉非常新鲜。作为一种界面编程语言，markdown比HTML简单很多，熟悉了markdown之后再写文档，可以使文档排版更为美观。  

我现在对markdown的使用还不甚熟悉，希望在以后的实验中能渐渐地熟悉起来