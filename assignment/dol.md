##DOL实例分析&编程 实验报告##

###DOL简介
Distributed Operation Layer(DOL)是一种用于编码分布式操作的应用框架，DOL可以自动地将应用映射到多和处理器的平台上，DOL共包含以下三个基本组成成分：

- **DOL Application Programming Interface**
- **DOL Functional Simulation**
- **DOL Mapping Optimization**

###实验步骤 
根据实验要求，修改example1的xml文件，将迭代次数改为二
   
    <variable value="2" name="N"/>

修改example1的square.c文件，将输出赋值为输入的立方

	
	int square_fire(DOLProcess *p) {
    	float i;
	    if (p->local->index < p->local->len) {
	        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
	        i = i*i*i;
	        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
	        p->local->index++;
	    }
	    if (p->local->index >= p->local->len) {
	        DOL_detach(p);
	        return -1;
	    }
    	return 0;
	}


重新编译运行
>     $	ant -f runexample.xml -Dnumber=1
>     $	ant -f runexample.xml -Dnumber=2


###实验结果展示 
实验1的运行结果<br>
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/dol/dol_1_result.jpg">

实验2的运行结果<br>
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/dol/dol_2_result.jpg">

实验1的dot截图<br>
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/dol/dol_1_dot.jpg">

实验2的dot截图<br>
<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/dol/dol_2_dot.jpg">

###Experimental experience
这次实验的整个过程中有一些奇怪的小坑，譬如要删掉build文件夹中已经编译好的example文件夹，再次编译运行时才会正确地显示出实验结果。另外，由于这次实验
在很早之前就完成了，因此写实验报告的时候都忘得差不多了。。。不过实验总体来说还是非常简单的，TA给的PPT里面解释地非常详细。而且TA上课蛮风趣的。
