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

# 2024年10月15日

本来这些内容我应该在13号或者14号就发布了，但是，我在14号寄出给法院的信件后回到住所刚想稍微休息一下就非正常入睡了，在下午连续睡了几个小时，醒来后已经是晚上了，并且我发现手机有被改动过，在我的住所他们也可能采集了我的精液。也不排除他们在我本人陷入睡眠期间对我的身份进行了冒用。

在14号以前的这段时间，这些攻击者反复影响我的睡眠，导致我在白天进行操作时的状态极差，这也导致我在寄给法院的一份文档上出了错。好在，我在14号应该已经成功进行弥补。

14号的攻击应该是化学手法的麻醉气体，也可能是在我的食物里下了药。他们本来已经很少会用这种手法了，他们在14号之前一直比较常见的是另一种我还没有完全想明白的非常难以察觉的攻击手段。我后来发现他们的攻击技术是随着我的防护技术的提升也是在不断改进的，我在[2024年6月1日提到的帽子](https://github.com/YongBinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn/blog)早已经失去了防护作用。于是我后来又改了另一版本。另一个版本我在13号进行了测试，在13号佩戴第二版帽子期间没有发现自己遭受到那种难以察觉的攻击的痕迹。我想，第二版帽子在13号的测试成效可能是我在14号遭遇化学方法攻击的原因。

这些攻击者早就说过，我对于他们来说是透明的。透明的意思是我对于他们来说没有秘密，他们读取复制了我的记忆，并且可以监控我的想法。所以我在这两天的一些设想和计划可能已经被他们抄袭并先一步通过喉舌发布了，不过没关系，我哪怕被监控导致慢了一步，我也要把一些想法和意见发表出来。如果有人指责我抄袭，那我正好可以多发现他们的一些喉舌。

本来这段内容我想更隐晦的通过暗示藉由AI的口来说出来的，但是我今天改主意了。我想说的直白一点。他们就是一群人类中的垃圾，在指责我这个比他们要好得多的人。他们指责我过去做过这个做过那个，但是他们自己却不敢被以同样的方式审判，因为在他们的内心深处，他们明白他们自己其实根本比不上现在这个被攻击的人，他们比不上我。他们只要没有智力问题，就也应该能够清除的意识到，我并不是他们所指控的大部份问题的真正过错方。我就是比他们所有人都强，我比他们所有人都好，我敢和这些人作比较，但是他们却不敢遭受同等的审视，因为审视的结果只可能是发现我原来才是最好的那个。更何况，以他们正在对我进行的偷窃和骚扰，不难推断，他们是有能力伪造很多所谓“证据”的，这些“证据”对于我来说很容易反驳，也正因如此，他们在极力避免给我为自己辩解的机会，想方设法让我没有机会发出声音。

还有小道消息称，有人特意找了一些不懂法的人来对我投票判决。我正好让AI"为那些对法律一无所知的人解释一下为什么需要程序正义，以及为什么要排除非法证据"，我也懒得复制粘贴了，“程序正义”和“非法证据”是很成熟的概念，看到了本笔记却不知道这两个概念的人，应该自行询问AI或者查询wiki。

----

关于技术方面，我在上周六移除了电脑自带的SSD，但是发现装到硬盘盒里后无法启动了。我后来尝试了多种途径解决这个问题，包括在windows下让qemu打开`\\.\Device\Harddisk0\DR0`但是，qemu在这方面兼容做的不好。后来尝试改注册表让windows匹配windows to go，可惜换了个错误代码还是无法启动。后来我又尝试了一下在windows 10上用过的技巧，在linux下通过虚拟机让安装程序以为正在安装到固定硬盘，但可惜的是windows 11在我的虚拟机上无法启动，可能是微软增加了相关检测。我想可能我接下来会更多用Linux的live环境了，因为我基于HBCD改的PE系统无法安装打印机的驱动程序，或许更闲下来会尝试搞个全功能的windows live dvd。

我的pinephone pro出现了奇怪的问题，小道消息说是手机上安装了恶意硬件通过uart让攻击者访问控制台。

所以我上周在刷系统的时候做了如下处理：

```shell
gzip -d -c mobian-pinephonepro-phosh-12.0.img.gz | sed "s|ttyS2|wyee0|g"|sudo dd of=/dev/sdb bs=4M status=progres
````

但是哪怕是通过这样的手段移除有关ttyS2的配置，我的PinePhone Pro的init进程仍然在为了ttyS2启动agetty，这让人费解。

----

这帮孙子现在最喜欢用的攻击手法还是那几个，我最近遭受到的攻击也还是这些：

 * 在数据线的头部进行破坏，让破坏痕迹看上去像是自然弯折损耗
 * 通过这些手段让受害者不得不频繁充电，难以自由行动：1. 把受害者的锂电池更换成更低容量的(我的Oneplus 5T的电池就被换成低容量的了，电池我没换过，但是手机设置里显示的容量低于出厂电池的容量（不是折算健康度之后的值）；我的游戏机前两天也被换了，电池突然从可以坚持4个小时变成只能坚持1小时左右了) 2. 对受害者充满电的设备进行完全放电，以此降低受害者设备的电池寿命 3. 在受害者充电时，通过手机上的木马进行高强度运算或者其他技术途径让充电无法充满。
 * 偷窃和破坏其他能够为受害者带来防护和效率的物品

其中值得一提的是，我放在枕头下的一截大概1.5米的三股实心铜缆电源线被盗了，这说明这小段铜电源线很可能干扰了他们对我脑部的攻击。



# 2024年10月19日

我在制作新项目[cursed_live_dvd](https://github.com/YongBinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn/cursed_live_dvd)的过程中持续遭到攻击，昨天发生了一个奇怪现象,只要iso被编辑好qemu成功系统，u盘就会被直接弹出，导致iso文件无法完全写入。今天刻好盘，在grub菜单时，我按下e编辑启动参数，然后我就什么都没做，光驱自己弹出了。当时电脑没有连接电源和网络。由此推断，应该是有恶意硬件配合了恶意固件。恶意程序在grub之前就已经启动，所以很有可能是在uefi，并且还有个配套的恶意硬件帮助无线收发命令。而这种恶意硬件应该是有距离限制的，而我就自己一个人在自己的住所，所以攻击者当时有可能就身处我周围的房间，或者有无人机之类的东西帮忙把信号传递到远处。为什么我判断有恶意硬件而不是恶意程序利用了电脑自身的硬件呢？因为这台笔记本电脑的无线网卡是我亲手拆下来的,它的蓝牙功能也是由这个无线网卡支持的。

至于说如何揪出这种恶意硬件，已经有人给我指了一条路，那就是TinySA Ultra。考虑到这个东西有点敏感,尤其我又是身处他国，我想在购买之前先消除不必要的误会和隐患，所以我已经多次发邮件询问瑞士当地管理部门是否允许我购买使用这个设备，但是一直没有得到任何回复。可惜，如果我有了这个设备，应该能揪出那个恶意硬件。

他们这样得手，是否是我技术不行呢？不是。因为所有的安全举措都是有假设的前提条件的，比如说一个大学可能会雇用一些保安实施一些安全防范措施，这些措施大多数是针对社会一般人员的，比如说有人可能来偷学校里的东西或者有人可能会在学校里打架，但是这些安全措施如果遇到美军用轰炸机和坦克来攻打校园了或者遇到解放军用洲际导弹来炸学校了，那这些措施和没有安全措施是差不多的。这并不是学校的安全措施不行或者安保人员的技术水平不够，而是从威胁模型和现实不匹配。我的信息安全技术和相关安全措施的假设条件是对方无法物理接触我的设备，而这个犯罪团伙应该是物理方式接触到了我的设备，所以这不是我的技术不行，而是我学习研究的是信息安全技术而对方使用的是开锁技术和偷窃技巧。对方不是很厉害的黑客，而是团伙作案，是使用队友给他的恶意软件安装程序的，很有经验的贼。

# 2024年10月21日

制作新项目的过程中，我仍然是持续遭到攻击，这次的现象我拍照录像了:

先是无法启动:

![img](https://github.com/YongBinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn/i_am_hacked/blob/6f615f1baf8c8ce32d03ebd246f00b15981ced35/photos/2024-10-21%20bios_shim_SBAT_failure.JPG)

然后是无法保存iso文件到u盘:

[录像文件地址](https://github.com/YongBinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn/i_am_hacked/raw/6f615f1baf8c8ce32d03ebd246f00b15981ced35/recordings/2024-10-21%20unable_to_save_cursed_project_iso_file.mp4),录像中我无法把iso复制到u盘里，总是在写入快要完成时u盘设备莫名出错。我复制了好几次都是这样的结果。

后来刻录iso到光盘的时候也莫名出错了一次。

可以推测,有时候我项目中提交的代码会莫名其妙的多出来一些[低级失误](https://github.com/YongBinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn/cursed_live_dvd/commit/cc82bb2d51b4b0940d0625b7385642ac17d1636b)可能不是我粗心大意，而是被人暗中使坏了。

我的生活总是像这样在别人看不见的地方出现的阻碍，拖慢我的速度、浪费我的时间、消耗我的精力。如果有人正在通过邮件联系我，他们只会感到我回复邮件很慢，好像对他们的事不够重视，但是他们并不知道我为了能够正常启动电脑都花费了很多时间。


# 2024年10月23日
我针对我的论文成绩起诉我的学校可能无法继续了。期间的经历非常违反人们认知中的常识。比如说卢加诺当地的法院明明已经开始向我收取相关费用，却又马上拒绝了我的上诉。我接下的几天应该会整理发布出来我在为了寻求公正的评分的过程中，我与学校以及与法院之间的通讯内容。

# 2024年10月24日
懦夫，你们这帮人在向我展示权力，但是你们也向我展示了你们的懦弱和恐惧。你们只敢于躲在一众人当中暗中使坏然后假装自己很勇敢。举例来说，你们甚至不敢让法院给我立案。只要立案，你们就有了被反驳倒的可能性，而且你们心理对我的评估告诉了你们，立了案之后我回应，所以你们怕了，你们不敢让立案发生了。而那个有钱弱智在假装自己很勇敢的小声悄悄说"all in"的时候，他既没有all in也没有赌，因为那时法院的结果已经出来了而他已经看到了。已经看到了阻止了我立案，才敢悄悄的说一声all in，甚至不敢让别人知道阻止立案的就是他。

你们所谓的决斗和对决只敢在我没有办法反抗的情况下动手，因为你们怕，你们知道平等对决你们会输。就好像人们为了抓住一只瓢虫就敢于直接上手，也不会多余的戴上什么防具。而如果人想要摸到一只能够杀死他们的野兽的时候，就只能先使用麻醉枪让它反抗不了之后再做足了防护才能下手。这两者之间的差距就是怕与不怕的差距，就是对手在你心中的危险程度的差距。所以，不用假装你们不怕我了，我已经看穿了。

紧跟着是另一个曾经的有钱象征的实际精神病和他一起配合打算连这个GitHub帐号一起给我坑了。连锁攻击配合的不错，但是仍然改变不了你们在我心中假装勇敢的懦夫形象。
