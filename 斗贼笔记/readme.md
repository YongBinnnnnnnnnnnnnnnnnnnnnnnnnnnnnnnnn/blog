笔记从2024年9月12日开始在这里续：

# 2024年9月12日

这两天终于感觉脑袋没有之前那么缓慢了。更新一些新发现的对方的攻击手法


## 隐蔽拍摄

### 关于一种微小摄像头的猜测

对方有及其微小的摄像头，可以小到安装在蜘蛛的身上。这种程度的科技应该是国家级别的间谍或者军事科技。

这种摄像头也可以安装在人体上，比如脖子或者脑门处，外观可能就是一颗痣或者一个小红包，但是却可以让对方当摄像头用。

## 关于房间内监控的观察

我观测到类似红外摄像头的行为，在我刚刚购买了红外感应门铃时，有一天我无意间把门铃对上了卧室的一个角落，然后这个门铃就发生了一个奇怪的现象：每隔五分钟想一次铃，因此怀疑是有一种极小到肉眼很难发现的红外摄像头被设置成每隔5分钟取一次画面。这样即便是用红外探测设备也很难发现因为取画面也只是一瞬间，而为了捕捉到那一瞬瞬间，红外探测设备要一直探测才行。这个现象我观察到之后当天出了一次门再回来就没有了。推测是我出门期间骚扰者进入了我的住所对摄像头进行了调整。

### 小道消息

根据小道消息，对方已经停用红外摄像头改用紫外摄像头和X光了，并且这种设备可以看穿木头，所以摄像头可以在完全不露出镜头的情况下进行监控。

## 失去意识

目前对于短时间失去意识的最新猜测是，对方使用了EMP对脑部进行攻击。因为已经观察到多次在卧室中发生电力设备在未被外力干涉的情况下被损毁而且损毁只是让它停止工作而没有外伤，这很像是EMP的结果。目前没有找到很好的防范策略。同时这个假说还有一个缺陷，那就是为什么被影响的只是电力设备：充电头和UPS和我放在地上的红外感应门铃,而手机电脑却没有被EMP干扰。

虽然小道消息一再告诉我对方让我失去意识的手法是声波，并且还给我看了一个视频演示声波让人说不出来话 ( [Testing My Speech Jammer In Public | YouTube](https://www.youtube.com/watch?v=J-SH18dtBlY) ) 但是从视频来看，这种攻击类似于我遭受过的一种可以被我发现和感知的攻击手法，而攻击者还存在另一种极难被感知到的让人暂时失去意识的手法，这个手法我推测是EMP。

# 2024年9月13日

今天去inlingua店面询问为什么我发送的邮件没有回复，对方现场找邮箱发现没有收到，于是我在现场把我之前发给他们的邮件重新转发了一遍，收件地址都没变，他们当场就收到了。这件事我认为有三种可能性：

1. 有人黑入了inlingua的系统，删掉了邮件。
2. 有人雇佣了inlingua的内部员工让他瞒着所有人偷偷把我的邮件删了
3. inlingua的邮件系统的所属公司与骚扰者形成了合作关系。

今天醒来后发现可能又有人用什么机械够到我了，身上一些地方有了本不该出现的污垢，出门前擦拭了一遍身体，感觉闻不到臭味后才出的门，但是出门后发现周围人的反应好像我的身上还是有味道，这说明我的鼻子很可能也被麻醉了，导致我闻不到身上的异味。

同时晚上睡觉的录像显示手机慢慢滑落导致录像出现了一小段看不见的情况，这个表面上的意外很可能并不是意外而是闯入者把手机故意放倒的，因为手机不倒下他们篡改录像画面后很难准确把手机放回原位。所以干脆就让手机倒下再篡改画面做个手机慢慢滑落的假象。同时今天起床后发现iphone 6s有被人拆开过的痕迹，但是晚上的录像却显示什么都没发生，这让我想报警也有些难办。

# 2024年9月23日
AI写代码不太行，有些细节把握不好，还制造很多bug，不过我看好它的前景，只是现阶段还无法取代程序员

我给AI的提示：

```
帮我写powershell脚本，启动chrome.exe后读取其内存，找到内存中的google.com字符串并改写内存数据替换google.com为ybnxdomain。不要用psexec，用windows api，readprocessmemory和writeprocessmemory，启动进程用createprocessex
```

AI的结果：

``` powershell
# 加载必要的库
Add-Type -AssemblyName System.Windows.Forms
Add-Type -TypeDefinition @"
using System;
using System.Runtime.InteropServices;

public class MemoryHelper
{
    [DllImport("kernel32")]
    public static extern IntPtr OpenProcess(int dwDesiredAccess, bool bInheritHandle, int dwProcessId);

    [DllImport("kernel32")]
    public static extern bool CloseHandle(IntPtr hObject);

    [DllImport("kernel32")]
    public static extern bool ReadProcessMemory(IntPtr hProcess, IntPtr lpBaseAddress, out byte[] lpBuffer, int nSize, out int lpNumberOfBytesRead);

    [DllImport("kernel32")]
    public static extern bool WriteProcessMemory(IntPtr hProcess, IntPtr lpBaseAddress, byte[] lpBuffer, int nSize, out int lpNumberOfBytesWritten);
}
"@

# 定义 Chrome.exe 的路径
$chromePath = "C:\Program Files\Google\Chrome\Application\chrome.exe"

# 启动 Chrome.exe
$processId = Start-Process -FilePath $chromePath -PassThru

# 等待 Chrome.exe 加载完成
Start-Sleep -s 5

# 查找 Chrome.exe 的进程句柄
$handle = [MemoryHelper]::OpenProcess(0x001F0FFF, $false, $processId.Id)

if ($handle -ne 0) {
    # 定义要查找的字符串
    $targetString = "google.com"

    # 定义替换的字符串
    $replaceString = "ybnxdomain"

    # 分配内存缓冲区
    $bufferSize = $targetString.Length * 2
    $buffer = New-Object byte[]($bufferSize)
    [Runtime.InteropServices.Marshal]::Copy([Text.Encoding]::Unicode.GetBytes($targetString), 0, $buffer, 0)

    # 查找内存中的字符串
    for ($offset = 0; $offset -lt (Get-WmiObject -Class Win32_Process -Filter "ProcessID=$processId.Id" | Select-Object -ExpandProperty VirtualSize)) {
        if ([MemoryHelper]::ReadProcessMemory($handle, [IntPtr]$offset, out $buffer, $targetString.Length * 2, [ref]$null)) {
            $stringFound = [Text.Encoding]::Unicode.GetString($buffer)
            if ($stringFound -eq $targetString) {
                # 替换内存中的字符串
                [MemoryHelper]::WriteProcessMemory($handle, [IntPtr]$offset, $([Text.Encoding]::Unicode.GetBytes($replaceString)), $replaceString.Length * 2, [ref]$null)
                Write-Host "已替换内存中的字符串：$targetString -> $replaceString"
            }
        } else {
            break
        }
        $offset += $targetString.Length * 2
    }

    # 关闭进程句柄
    if ([MemoryHelper]::CloseHandle($handle)) {
        Write-Host "已关闭进程句柄"
    } else {
        Write-Host "无法关闭进程句柄"
    }
} else {
    Write-Host "无法打开进程句柄"
}
```

