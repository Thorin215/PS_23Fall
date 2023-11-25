---
title: Lab0 of CTF
date: 2023-07-05 10:11:32
tags:
---


# <center>Lab0</center>

<center> Thorin </center>
---

## 1.1 Challange1

<center>

*在kali-linux-2023上进行* 
</center>

### 1.1.1 路径相关命令

```shell
cd filename
cd ..  #上一级路径
cd ~   #home
cd .   #当前路径
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%871.png)

### 1.1.2 文件目录操作命令

```shell
ls -a #列出所有文件和目录
ls -l #列出详细信息
touch file #创建文件
mkdir dir  #创建目录 
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%872.png)

### 1.1.3 文件内容查看命令

```shell
cat file 
head -n lines file #显示前lines行
tail -n lines file #显示后lines行
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%873.png)

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%873.png)


### 1.1.4 其他命令

```shell
whoami   #获取当前用户
date     #获取当前时间
ps       #显示进程信息
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%875.png)

## 1.2 challenge2

### 1.2.1 解释代码

```py
#!/usr/bin/python3

data = input("give me your string: ") #data存储输入
print("length of string:", len(data)) #输出data长度
  
data_old = data                       #存储未更新的data
data_new = ""                         
for d in data:                         
    if d in 'abcdefghijklmnopqrstuvwxyz':    #大小写互换后存入data_new
        data_new += chr(ord(d) - 32)
    elif d in 'ABCDEFGHIJKLMNOPQRSTUVWXYZ':
        data_new += chr(ord(d) + 32)
    else:
        data_new += d                       #非字母不修改

print("now your string:", data_new)          #输出结果
```

### 1.2.2calculator

```py
import socket

lPOST = '10.214.160.13'
rHOST = 11002
client_socket = socket.socket()
client_socket.connect((lPOST, rHOST))

while 1:
    data1 = client_socket.recv(1024)
    data2 = client_socket.recv(1024)
    print(data1)
    print(data2)
    new_data = data2[:-2]
    print(new_data)
    client_socket.send((format(eval(new_data))+'\n').encode())
    print(format(eval(new_data)).encode())
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%876.png)

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%877.png)


<center>

`AAA{melody_loves_doing_calculus_qq_qun_386796080}`
</center>

## 2.1 Crypto

```py
    for i in range(4):
        for j in range(4):
            result[i][j] = s[i][j] ^ k[i][j]
```

```py
   for i in range(4):
        for j in range(4):
            result[i][j] = inv_s_box[s[i][j]]
```

![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%878.png)

<center>

`AAA{AE5_aEs_a1s}`
</center>

## 3.1 Misc



![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%879.png)

<center>

`AAA{wELCOm3_7o_CTf_5umMeR_c0uR5E_2023}`



![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8710.png)


![](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8711.png)

` AAA{gr3@t_J08!_1et’5_P1@y_m1S C_TOG3Th3R}`
