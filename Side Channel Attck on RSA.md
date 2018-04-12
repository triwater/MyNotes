# Side Channel Attck on RSA

## 简介

RSA算法是一种常见的非对称加密算法，因此很多人都想法设法去破解它，但是当RSA使用的质数位数很大时，进行大数分解是一件很难的事。但是总有一些人会另辟蹊径，使用侧信道攻击破解RSA的私钥。

## RSA的过程

分为三个算法，密钥生成、加密、解密：

1. 找到互质的两个数, `p` 和 `q`, 计算 `N = p*q`
2. 确定一个数 `e`, 使得 `e` 与 `(p-1)(q-1)` 互质, 此时公钥为 `(N, e)`, 告诉给对方
3. 确定私钥 `d`, 使得 `e*d-1`能够被`(p-1)(q-1)`整除
4. 消息传输方传输消息 `M`, 加密密文`C`为: C=M^e mod N
5. 消息接受方通过收到密文消息 `C`, 解密消息 `M`: M=C^d mod N

其中前三步是密钥生成，第四步是加密，第五步解密。

## Timing Attack

从上面可以看出，加密和解密都需要使用幂模运算，也就是x = a^b  mod  n，这里a是密文，b是私钥， n是质数乘积，因为这些数都特别大，所以直接计算的话会很慢，所以一般在这里都会对该运算做一些优化，例如蒙哥马利算法：

```java
int mod(int a,int b,int n){  
    int result = 1;  
    int base = a;  
    while(b>0){  
     if(b & 1==1){  
         result = (result*base) % n;  
      }  
     base = (base*base) %n;  
      b>>=1;  
   }  
   return result;  
}
```

这个算法是从b的最低位循环到高位，如果是1的话进行两次运算，是0的话进行一次运算，而由于这个算法比较耗时，所以攻击者通过构造不同的输入便可以猜出私钥的某一位是0还是1。

但是事实上，目前很多语言都使用了延迟返回的方法来规避此类的攻击。举个例子：

```python
def safeEquals(a: String, b: String) = {
  if (a.length != b.length) {
    false
  } else {
    var equal = 0
    for (i <- Array.range(0, a.length)) {
      equal |= a(i) ^ b(i)
    }
    equal == 0
  }
}
```

这样一位一位比较的话，即便是发现两数不相等也不会立即返回false。

## 其它破解私钥的思路

主要参考ctf比赛中的一些思路

### 暴力分解

当使用的密钥长度比较短的时候用这种方法，还有一些网站比如factordb或者一些工具比如yafu可以查询。

### 共模攻击



## 参考资料

1. https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/lecture-notes/MIT6_858F14_lec16.pdf
2. https://www.stanford.edu/~dabo/papers/ssl-timing.pdf
3. https://www.anquanke.com/post/id/84632
4. http://diamond.boisestate.edu/~liljanab/ISAS/course_materials/AttacksRSA.pdf
5. https://err0rzz.github.io/2017/11/14/CTF%E4%B8%ADRSA%E5%A5%97%E8%B7%AF/