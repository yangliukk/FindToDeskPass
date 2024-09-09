# FindToDeskPass
通过Dump内存读取ToDesk设备代码、连接密码

测试版本：官网最新版4.7.4.8

# 通过Procdump 导出 ToDesk内存
首先查看ToDesk进程PID
```
tasklist /svc
```
![image](https://github.com/user-attachments/assets/be83f90c-a750-4816-8fdb-9393fca32346)

这里存在两个ToDesk进程，我们选择非`ToDesk_Service`的PID

```
procdump64.exe -accepteula -ma 856
```

将Dump下来的文件使用编辑器打开

直接搜索当前日期，今日是2024年9月7日，所以搜索`20240907`。找到一个长度为14位的字符串，该字符串规律：当前日期+重置密码次数（随机值累加）

设备代码紧跟着这串长度14的字符串，图中也就是`973656xxx`

连接密码在上方约224个字节位置。此处为`k4zeus0z`

![image](https://github.com/user-attachments/assets/dd5c181b-67b9-4d17-898a-c7877191478b)

---------------------------------------------------------------------------
2024年9月9日补充
根据吐司论坛QAdmire师傅的反馈，4.7.4.3版本该位置对应不上（猜测该版本该位置为安装时间）

不过还是可以搜索当前日期（黄色箭头指向），往上寻找发现密码

![image](https://github.com/user-attachments/assets/5293a037-55ca-421e-aa30-214eec7700a7)

不过我在4.7.4.8版本依旧是原来位置，反倒是更下方位置为安装时间

所以猜测是版本不同带来的差异

![image](https://github.com/user-attachments/assets/d2cbd9cc-8e91-41b9-8322-70ad69cda2ae)



## 使用安全密码也可读取
方法一样，直接贴图
![image](https://github.com/user-attachments/assets/2c284453-9429-49e3-afe7-c065e0238bb1)

![image](https://github.com/user-attachments/assets/2c846140-d01f-4488-9c89-10426ea87635)
