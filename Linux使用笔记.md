# Linux使用笔记

现在有了两台台式机，在一台台式机真机上装了ubuntu 17.10，工作效率直线飞升。但是鉴于之前都是在虚拟机里跑ubuntu，没怎么用真机，操作不甚熟练，加上17版本加了很多新特性，所以这里记录一下使用中遇到的坑以及解决办法。前几个没啥印象了，所以就简单写一下。

1. 修改环境变量: sudo gedit /etc/profile，在文件最后添加export PATH=~/mypath/bin:$PATH，保存后source /etc/profile生效。因本人用不惯vim，最顺手的用着就好啦
2. ubuntu 17版本执行上面的指令有时候会报错，具体报错信息忘了，大概意思就是没权限（？），解决办法是输入指令xhost +
3. 录屏，ubuntu17上只有green recorder能用，支持区域录屏，还不错，唯一的缺点是输出的格式只有webm，需要转换一下，具体的指令是 ffmpeg -i in.webm -s <width>x<hight> out.mp4
4. 安装android fastboot工具： sudo apt-get install android-tools-fastboot   ps：我用fastboot 刷入factory image的时候，老是提示我fastboot is too old，可我明明从google官网下的最新版，谷歌对linux的支持很不好
5. 安装openjdk7： 网上其它说的做法都不管用，参考这个问题的第二个回答：https://askubuntu.com/questions/761127/how-do-i-install-openjdk-7-on-ubuntu-16-04-or-higher
6. ​算是一点感想吧，打jar包到服务器上跑，因为这个东西比较耗时耗内存，所以需要弄个监视进程监视一下java进程的状态，太耗时就给他干掉，这几天抽空学习一下python监视脚本。
7. docker：做了一道CTF题需要docker的环境，之前没接触过。主要参考https://yeasy.gitbooks.io/docker_practice/content/ 
  几个简单的命令:docker image ls; docker run <name of image>
8. scp命令
9. adb devices的时候no permissions (user in plugdev group; are your udev rules wrong?)
  github上有个项目说这个的https://github.com/M0Rf30/android-udev-rules
  但是我试了一下不行,最后关掉usb调试再打开就ok了
