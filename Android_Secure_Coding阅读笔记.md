# Android_Secure_Coding阅读笔记

## 简介

最近看了《Android Application Secure Design/Secure Coding Guidebook 》这本书，觉着不错，这本书主要写给安卓开发者，当时作为应用安全研究人员也可以看看，提供一些挖洞的思路。这篇笔记里面我主要写的是我之前不知道的东西。

## 四大组件的使用

1. 不要指定launchMode，因为有的非standard的launchMode指定了之后会新建一个TASK，这样其它应用就能获取到应用发出的Intent了，同理也不要在Intent上设置FLAG_ACTIVITY_NEW_TASK的FLAG。
2. 启动Activity的时候要设置清晰的Intent，不要使用intent.setClass这种方式，因为这样如果一个Malware伪造了包名，那就可能导致钓鱼了。
3. Fragment注入攻击，比较老了，现在应用用的估计也不多。
4. 使用动态广播时候需要注意，动态注册的广播默认是exported的。
5. ​
