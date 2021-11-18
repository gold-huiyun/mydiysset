<h1 align="center">青龙JD小知识合集</h1>

## 内部助力脚本配置
### 1.添加助力脚本文件有很多方法，只列举几个

  法(1)：

使用某塔面板的文件管理功能或者MobaXterm、FinalShell等等ssh工具的文件管理功能

把`code.sh`和`task_before.sh`这两个文件上传到 `root/ql/config`目录下（task_before.sh有空文件需要覆盖）

  法(2)：

使用青龙面板脚本管理功能.

点击+号新建脚本，命名`code.sh` 确定后，点击退出编辑脚本，调试-保存-保存目录填`/ql/config`确定

青龙默认配置文件目录有task_before.sh文件无需新建


然后回到青龙面板配置文件处右上角可以选择文件
将code.sh和task_before.sh两个空脚本，依次分别填入对应内容，保存即可

  法(3)：使用青龙在定时面板执行,含有以下内容的.sh脚本
```
cd /ql/config
wget https://ghproxy.com/https://raw.githubusercontent.com/gold-huiyun/mydiysset/main/qlhelp/code.sh -O code.sh
wget https://ghproxy.com/https://raw.githubusercontent.com/gold-huiyun/mydiysset/main/qlhelp/task_before.sh -O task_before.sh
```
在脚本管理新建脚本命名`getcode.sh`填入以下内容保存，添加定时任务:（名称:`getcode.sh`(可随意)命令:`task getcode.sh`定时规则:`30 0 6 8 *`）手动运行即可，运行结束后此定时任务删除即可

### 2.设置助力脚本定时任务，定时任务添加:

名称:code.sh(可随意)

命令:`task /ql/config/code.sh`

定时规则:`30 * * * *`

保存后先手动运行一次（如果助力活动的JD脚本没有运行过，日志中没有助力码，第一次运行可能无法获取到你的助力码，第二天就会正常获取到了）

此文件默认优先助力前面的Cookie（可以通过环境变量-名称，排序查看先后顺序），如需使用随机互助或均等互助，在青龙面板-配置文件-code.sh，第38行按照注释修改保存

**注意**:环境变量中填写的JD的COOKIE不能使用换行隔开，必须要用&或者一个变量设置一个cookie.

如果code.sh日志超线程报错可尝试将配置文件-code.sh中第23行适当调大一点
```
## 本脚本限制的最大线程数量
proc_num="7"
```


##### 未完待续......


# 结尾

本文部分内容借鉴于其他作者旧版教程，在此表示感谢。
[inoyna12有关code.sh的设置](https://github.com/inoyna12/JDsc/blob/main/backUp/code.md)

**注：本教程仅供学习交流使用,请勿用于非法行为！**

<details>
<summary>我不信还有</summary>
   
😭😭😭真没了。。。。。
   
