# Windows Server 2008 R2 安装 VMTools 后系统自动重启

虚拟机使用**完整模式**安装`vmtools`之后，系统出现自动重启的情况，罪魁祸首 BSOD [^bsod].

##### 系统错误日志

> 事件1:
> 
> 来源：BugCheck
> 
> ID：1001
> 
> 常规：计算机已经从检测错误后重新启动。检测错误: **0x0000000a** (0x0000000000000350, 0x0000000000000002, 0x0000000000000001, 0xfffff800016c55f3)。已将转储的数据保存在: C:\Windows\MEMORY.DMP。报告 ID: 012116-6910-01。
> 
> 事件2：
> 
> 来源：Kernel-Power
> 
> ID：41
> 
> 常规：系统已在未先正常关机的情况下重新启动。如果系统停止响应、发生崩溃或意外断电，则可能会导致此错误。

##### 处理

step1, 搜索定位`0x0000000a`错误范围在设备驱动错误

step2, 错误之前的操作是完整模式下安装了`vmtools`

step3, 找到同样的[案例](https://blog.brankovucinec.com/2014/05/19/windows-server-guest-gets-bsodbugcheck-on-vmware-esxi-5-5-and-5-5u1/) ,是因为安装了`vmtools`中的 **VMCI Driver**导致

final, 控制面板修改`vmtools`程序，卸载VMCI组件

##### 相关链接

[Windows Bugcheck Analysis](http://social.technet.microsoft.com/wiki/contents/articles/6302.windows-bugcheck-analysis.aspx)



[^bsod]: Blue Screen  of Death

