---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shikiji
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: 首页
mdc: true
---

# 机顶盒事业部朱梦园

## 2023年工作总结及2024年工作规划

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/rezhu001/Enable" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# 23年大事记

23年七月时我正式入职，从此便开始了在GIEC的工作

- 📝 **graduation** - 从湘潭大学毕业，通过校招顺利进入杰科
- 🎨 **Production** - 为期一个月的生产流程实操
- 🧑 **Set-top box** - 回到工位，开始熟悉机顶盒事业部
- 🤹 **TS analysis** - 第一个任务——编写TS码流解析工具
- 🎥 **ALi_TDS** - 熟悉机顶盒操作系统
- 📤 **Customer Premise Equipment** - 接手CPE项目，开始全力投入其中
- 🛠 **To the future** - 渐入佳境，不断学习

<br>
<br>

Read more about [zhumy Gitlab](http://192.168.10.16/gitlab/zhumy)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
layout: default
---

# 目录

```c
//点击可跳转至对应界面
```

<Toc maxDepth="1"></Toc>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
level: 1
---

# 导航

鼠标移置左下角可打开导航栏

## 快捷键

|     |     |
| --- | --- |
| <kbd>right</kbd> / <kbd>space</kbd>| 下一步操作 |
| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | 上一步操作 |
| <kbd>up</kbd> | 下一页 |
| <kbd>down</kbd> | 上一页 |
| <kbd>o</kbd> | 整体预览 |
| <kbd>d</kbd> | 模式切换 |

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
layout: default
---

# TS analysis

### 柔性数组

```c {all|5|1-6|7,8|all}
//柔性数组的结构
typedef struct untreated_data       //存储一个TS包的数据
{
    unsigned int package_data_length;
    unsigned char untreated_data[];
}untreated_data;
//使用时先对其进行初始化
untreated_data *untreated_data_Path = NULL;
//对其进行内存分配和赋值
untreated_data_Path = malloc(sizeof (untreated_data) + package_length * sizeof (unsigned char));
memcpy(untreated_data_Path->untreated_data, packetbuffer, package_length);
untreated_data_Path->package_data_length = package_length;

```

动态数组的[内存分析](dist/assets/TS_parse/内存分析.drawio.png)

优点:  

- 可变长度数组，其大小随实际应用动态调整，简化内存管理
- 减少指针调用复杂性，在存储不定长数据时，比使用指针分配数组更加高效


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
layout: default
---

<style>
h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

## TS analysis
#### 动态链接库 .dll
```c {all|3|all}
//在.h文件中：
//外部函数 .dll文件总入口
_declspec(dllexport) int interface_main(const char* path);
//外部函数 用于测试是否成功调用 .dll
_declspec(dllexport) int dll_test();

//在函数定义时：
int interface_main(const char * path)
{
  //执行对应操作
  return 0;
}
```

- 其编译生成 descriptordll.dll 动态链接库，此时可以被其他函数动态加载（使用时加载，用完则释放）
- 将常用的处理逻辑进行封装，方便多个程序进行复用，同时共享 DLL 内存空间，节省内存
- 更时只需保证 API 接口一致，替换 .dll 文件即可完成单独功能的升级或替换
- 无需重新编译整个应用程序的情况下就可以更新特定的功能，使程序更加耦合，适应性更强。


---
layout: default
---

<style>
h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

## TS analysis
#### Python 联合编程

```python {all|2,5|7-9|12|all}

from ctypes import *                # 引入 ctypes

file_path_bytes = bytes(file_path, "utf-8")
lib = CDLL("./descriptordll")       # 动态加载

lib.dll_test()
lib.teststring(file_path_bytes, len(file_path_bytes))
lib.interface_main(file_path_bytes) # 调用.dll 中的 interface_main 函数

a = lib._handle
win32api.FreeLibrary(a)             # 释放动态链接库
print('.dll will be free')

```

- python 使用 ctypes 加载 .dll 动态链接库，并传入参数调用库中的 interface_main 函数
- 上层 GUI 界面使用 pyside 6 ，底层解析 TS 流逻辑使用 C 编写的 .dll
- 最终实现 UI 界面和程序逻辑的分离


---
layout: default
---

<style>
h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

## TS analysis 
#### MVC 软件架构 及 整体框架

<img src="dist/assets/TS_parse/MVC软件架构.png" class="m--25 h-125 w-auto rounded shadow" style="transform: translateX(530px);" />
<img src="dist/assets/TS_parse/MVC软件架构2.png" class="m--97 h-95 w-auto rounded shadow" style="transform: translateX(380px);" />


---
layout: default
---

<style>
h1, h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

# ALi_TDS
## ALi - M3711C 
### 开始正式练习 STB 项目时间并不长，很快接手了 CPE 项目，故产出较少，在学习期间，主要完成了：

- 学习了SVN 的使用，理解了SVN 和 git 的区别，拉取了对应板子 DVS-PTV-08G 的代码
- 将 STB 工程导入 Source Insight ，学习使用服务器编译代码下载烧录
- 阅读 ALi_TDS_SDK 手册，学习 ALi_TDS 操作系统启动过程
- 可变参数宏: ` _VA_ARGS_ `
- 拓展： `##_VA_ARGS_`
- 属性： `__attribute__(unused)`
- 符号表——（静态内存区）

---
layout: image-right
image: dist/assets/TS_parse/CPE.PNG
---

# Customer Premise Equipment > CPE

## CPE 项目于 2023/10/26 日正式释放 SDK 
<br>

#### 随后便开始熟悉OpenWrt操作系统，完成前期准备工作，软件功能测试、硬件适配、开发自己板子的程序、应用等  
<br>

#### 主要掌握了 docker、 Git 版本管理、Linux ( OpenWrt ) 命令、 shell、 Makefile、 .ipk安装包编译、.img 镜像生成、luci 架构 app 开发、lua语言等技能

<style>
h1, h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: default
---
## CPE-增加用户及密码修改
### 对应 shadow 文件：
```c {all|1|7，8}
root:$1$EAIaRTnR$rhSJPuT5DTd0w61K2dfso1:18724:0:99999:7:::
daemon:*:0:0:99999:7:::
ftp:*:0:0:99999:7:::
network:*:0:0:99999:7:::
nobody:*:0:0:99999:7:::
guest:$1$bcaMiQTu$35cPxaTASJj3cnKAe8LyJ0:0:0:99999:7:::
//其格式如下：
username:password_hash:last_password_change:minimum_days:maximum_days:warn_days:inactive_days:expire_date:reserved
```

- username: 用户名
- password_hash: 经过哈希处理的密码
- last_password_change: 上次修改密码的日期（从 1970 年 1 月 1 日开始的天数）
- minimum_days: 密码可更改的最短天数
- maximum_days: 密码有效期的最长天数
- warn_days: 在密码过期前提醒用户的天数
- inactive_days: 密码过期后多少天用户被禁用
- expire_date: 密码的过期日期（从 1970 年 1 月 1 日开始的天数）


---
layout: default
---
## CPE-对设备树修改(以GPIO为例)：
### 对应 codegen.dws 和 evb6890v_64_cpe.dws 两个文件：
```xml
<module name="gpio">
            <count>235</count>
            <gpio0>
                <eint_mode>true</eint_mode>
                <def_mode>0</def_mode>
                <inpull_en>true</inpull_en>
                <inpull_selhigh>false</inpull_selhigh>
                <def_dir>IN</def_dir>
                <out_high>false</out_high>
                <varName0>GPIO_EINT_RAMDUMP_PIN</varName0>
                <smt>true</smt>
                <ies>true</ies>
            </gpio0>
```
通过MTK TOOL python 脚本编译为 .dts 文件，在配置时，移远会对 GPIO 进行一层封装:
```c
static struct gpio_test_s gpio_test_table[] = {
  {18,73,GPIO_MODE_GPIO},  //PCIE_C_RST
  {21,75,GPIO_MODE_GPIO},  //PCIE_C_CLKREQ
  {27,70,GPIO_MODE_GPIO},  //PCIE_B_RST
  {39,133,GPIO_MODE_GPIO},  //WLAN_ACT
  //...
}
```

---
layout: default
---
## CPE-对设备树修改(以GPIO为例)：

### 同时需要包含对应的 .dtsi 文件：
```c
{
	model = "MT6890";
	compatible = "mediatek,MT6890";
	interrupt-parent = <&gic>;
	#address-cells = <2>;
	#size-cells = <2>;
	gpio_leds {
		compatible = "gpio-leds";
		led0 {
			label = "led9501:red:gpio";
			gpios = <&pio 209 GPIO_ACTIVE_HIGH>;
			linux,default-trigger = "none";
			default-state = "off";
		};
    //...
  }
  //...
}
```

#### 随后通过 Makefile 编译为 .dtb, 最后生成 .img 文件烧入板子


---
layout: default
---
## CPE-开机root登录：

```bash

  config dropbear
	option PasswordAuth 'on'
	option RootPasswordAuth 'on'
	option Port         '22'
#	option BannerFile   '/etc/banner'
	option RootLogin    '1'
	option MaxAuthTries '4'

```
<br>

## wan_lan自适应：
```bash
  uci set system.@system[0].quectel_main_uart='1'
  uci set system.@system[0].quectel_log_start='1'
  uci set system.@system[0].quectel_log_level='4'
  uci set system.@system[0].ql_wan_lan_auto_adapt='1'
  uci set system.@system[0].ql_wan_lan_auto_adapt_port0_disable='0'
  uci set system.@system[0].ql_wan_lan_auto_adapt_port1_disable='0'
  uci set system.@system[0].ql_wan_lan_auto_adapt_port2_disable='0'
  uci set system.@system[0].ql_wan_lan_auto_adapt_port3_disable='0'
  uci set system.@system[0].ql_wan_lan_auto_adapt_8221_disable='0'

```

---
layout: default
---

# LUCI 架构：
<img src="dist/assets/TS_parse/luci架构.png" class="m--5 h-110 w-auto rounded shadow" style="transform: translateX(200px);" />

<style>
h1, h2 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 0%, #146b8c 50%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>



---
layout: default
---

## LUCI_APP_slic 架构：

<img src="dist/assets/TS_parse/luci架构2.png" class="m--20 h-130 w-auto rounded shadow" style="transform: translateX(500px);" />
<img src="dist/assets/TS_parse/luci-app.png" class="m--100 h-100 w-auto rounded shadow" style="transform: translateX(420px);" />



---
layout: default
---

## LUCI_APP_wifi led修改：

```lua
function vif_disable(iface)
    os.execute("ifconfig "..iface.." down")
--wifi信号关闭时，新增判断
    local rai0_status = io.popen("ifconfig rai0 2>&1"):read("*a")
    local ra0_status = io.popen("ifconfig ra0 2>&1"):read("*a")
    local led_path = "/sys/class/leds/cpe_wifi_status"
    if rai0_status:match("BROADCAST MULTICAST") and ra0_status:match("BROADCAST MULTICAST") then
        os.execute("echo 0 > " .. led_path .. "/brightness")
    else
        os.execute("echo 1 > " .. led_path .. "/brightness")
    end

--
    luci.http.redirect(luci.dispatcher.build_url("admin", "mtk", "wifi"))
end
--wifi信号开启时，新增判断
function vif_enable(iface)
    local led_path = "/sys/class/leds/cpe_wifi_status"
    os.execute("ifconfig "..iface.." up")
--
    os.execute("echo 1 > " .. led_path .. "/brightness")
--
    luci.http.redirect(luci.dispatcher.build_url("admin", "mtk", "wifi"))
end

```


---
layout: default
transition: fade-out
---
# 杂项
<br>
<br>
<br>


## 1、C语言编程能力提升，编程思维更新
## 2、学习了回调函数的使用和编写
## 3、在 github pages 上部署了自己的 slidev
## 4、熟练掌握各种工具辅助解决编程问题
## 5、学习了网络挂载的开发方法
## 6、学会了 docker 的部署和使用
## 7、独立工作思考能力和与他人沟通能力提升

---
layout: default
transition: fade-out
---
# 2024年展望
<br>
<br>
<br>
<br>


## 1、深入学习Linux（OpenWrt）系统的各个模块
## 2、深入学习底层驱动的编写和实现
## 3、深入学习 luci_app 框架的开发
## 4、熟知 Linux 源码到镜像文件的生成过程
## 5、熟知各个模块，达到遇到问题深入底层分析
## 6、学习 Linux 系统中断，进程线程编程
## 7、学习 Linux 系统裁剪及其 内核移植

---
layout: default
transition: slide-up
---
# 致谢
<br>
<br>
<br>
<br>
<br>

# thanks

# 感谢各位