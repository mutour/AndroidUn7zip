AndroidUn7zip
==================

* A simple android ndk library used to simply extract lzma 7z files.<br>

* Some times we need to compress some resources in our applications,in some cases,LZMA 
 get smaller achieves than common zip,so we need extract the resources when the app 
start to run,this library is to do the work.<br>

###1.Introduction
* This is a small free library with simple function to extract the 7z file
* It is a jni call library
* This library is based on LZMA sdk,it does the most job.

###2.Usage

1. You can download all the demo source code and compile it.<br>
2. if you don't want to compile the c code, just use the library.

####Demo screenshoot
![image](https://raw.githubusercontent.com/hzy3774/AndroidUn7zip/master/images/screen.gif)
####JNI log
![image](https://raw.githubusercontent.com/hzy3774/AndroidUn7zip/master/images/jnilog.png)
####File manager
![image](https://raw.githubusercontent.com/hzy3774/AndroidUn7zip/master/images/file.png)
####Now Support Chinese
![image](https://raw.githubusercontent.com/hzy3774/AndroidUn7zip/master/images/log2.png)
####simple code:
    AndUn7z.extract7z(String filePath, String outPath);
    extractAssets(Context context, String assetPath, String outPath);
    
####2014-9-3 Add file chooser in demo project:
![image](https://raw.githubusercontent.com/hzy3774/AndroidUn7zip/master/images/screen1.gif)<br>
Thanks to ExfilePicker:https://github.com/bartwell/ExFilePicker

###3.Limitation
* 7z(LZMA) extract only
* not support password<br>
If you need more compress / extract functions or formats,https://github.com/hzy3774/AndroidP7zip

###4.More information
* More about it http://hzy3774.iteye.com/blog/2104510 <br>

###5.More about me
* [ITeye blog: http://hzy3774.iteye.com/](http://hzy3774.iteye.com/)
* [Baidu blog: http://hi.baidu.com/hzyws](http://hi.baidu.com/hzyws)
* [Sina weibo: http://weibo.com/hzy3774](http://weibo.com/hzy3774)

###6.Contact to me
* QQ: [377406997](http://wpa.qq.com/msgrd?v=3&uin=377406997&site=qq&menu=yes)
* Email: [hzy3774@qq.com](mailto:hzy3774@qq.com)


解决android x86 编译不过的问题，修改CpuArch.c文件的MyCPUID接口：
把：
  __asm__ __volatile__ (
    "cpuid"
    : "=a" (*a) ,
      "=b" (*b) ,
      "=c" (*c) ,
      "=d" (*d)
    : "0" (function)) ;
修改为：
__asm__ __volatile__ (
  #if defined(MY_CPU_X86) && defined(__PIC__)
    "mov %%ebx, %%edi;"
    "cpuid;"
    "xchgl %%ebx, %%edi;"
    : "=a" (*a) ,
      "=D" (*b) ,
  #else
    "cpuid"
    : "=a" (*a) ,
      "=b" (*b) ,
  #endif
      "=c" (*c) ,
      "=d" (*d)
    : "0" (function)) ;

