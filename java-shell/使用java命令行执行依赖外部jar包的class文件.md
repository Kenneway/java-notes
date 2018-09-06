很久没用Java的命令行来运行class了，今天拾回来这个，特此记录

 -Djava.ext.dirs=/wd/tomcat6/webapps/wcity/WEB-INF/lib/ 是class依赖的jar包的路径

java -Djava.ext.dirs=/path/to/jar/dir/ package-name.class-name


执行 java class 文件引入jar包

    执行某个Java编译后的class文件，一般是一个入口文件的时候，经常需要引入某lib包下的jar文件，方法如下：

java -classpath jar目录 class文件目录,eg:

java -classpath .:lib/* Run 

nohup java -classpath .:lib/* Run &

备注：上面命令中是将当前（Run.class）目录下的lib目录下的所有jar包引入



最简单的引用外部jar包执行，首先把src下的项目源代码打包成jar包，然后执行Java命令 ，class文件同理（先加载jar包，再找到main方法入口、传入参数）

java -classpath 引用jar包的路径(多个用;隔开,首先要把自身项目的jar包加载进来，然后才是外部引用jar包)  base.BaseDao 参数1 参数2

如：项目源代码jar包photo.jar包main方法所在路径base.BaseDao，引用jar包ojdbc6.jar，两个jar包在d:/bat目录下，则执行java命令

java -classpath photo.jar;ojdbc6.jar base.BaseDao enroll 2

1.clss文件

在docs命令下进入class所在目录或者直接把class文件拖拽进来，执行Java class文件名称或者全路径

如果Main方法包含参数，则在文件名称后写入参数如“：java Test 参数1 参数2 ...参数中间用空格分开

2.java项目（包含main方法的）

1）带包路径

首先编译成class文件，进入项目所在目录，找到bin文件夹；

如果要执行的main方法在自定义包下，则加上包名.类名执行，如：java base.BaseDao 

BaseDao所在的包为base，如执行带参数的和第一条执行方法一样

2）引用外部jar包

引用jar包需要把jar放入到bin目录下，解压然后重复第二条第1小节

3.jar文件

首先把java项目打包成jar文件，在打包成jar的时候注意，最后一步时可以写入Main Class也就是执行哪个类的main方法

（大概是因为如果有多个类的话不多个main方法时程序会不知道执行哪个）。在导出时写入Main Class可以避免在执行命令时报错。

如果导出jar没指定Main Class，需要在META-INF/MANIFEST.MF文件中写入：Main-Class: main方法所在的类路径  然后回车


1）没有引用jar包

和第二条的第一小条一样

在jar包目录下：

`java 包.类 args1 args2`

OR

`java -jar my.jar arg1 arg2`

2）引用了jar包

java -classpath jar文件;引用的jar文件，如：

`java -classpath base.jar;log4j.jar base.BaseDao`


如果项目引用的jar包比较多，可以把所有jar文件放入到一个目录中，例：

所有jar包在D:\lib目录下，需要执行：`java -Djava.ext.dirs=lib 包.类`就可以执行













