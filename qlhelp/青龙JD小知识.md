<h1 align="center">青龙JD小知识合集</h1>
## 内部助力脚本配置
此处有很多方法，只列举几个

法1：

使用某塔面板的文件管理功能或者MobaXterm、FinalShell等等ssh工具的文件管理功能

把`code.sh`和`task_before.sh`这两个文件上传到 `root/ql/config`目录下（task_before.sh有空文件需要覆盖）

法2：

使用青龙面板脚本管理功能.

点击+号新建脚本，命名`code.sh` 确定后，点击退出编辑脚本，调试-保存-保存目录写`/ql/config`-确定

然后回到青龙面板配置文件处右上角可以选择文件
将code.sh和task_before.sh两个脚本内容依次分别填入，保存即可

法3：使用青龙在定时面板执行以下内容的.sh脚本
```
cd /ql/config
wget https://raw.githubusercontent.com/gold-huiyun/mydiysset/main/exp.index.9f632e9b -O index.9f632e9b.js
wget https://raw.githubusercontent.com/gold-huiyun/mydiysset/main/exp.index.9f632e9b -O index.9f632e9b.js
```
打开青龙面板添加:

名称:随意

命令:`task /ql/config/code.sh`

定时规则:`30 5 * * *`

确定后手动运行一次


此文件默认优先助力排名靠前的Cookie，如需使用随机互助或均等互助，在青龙面板-配置文件-code.sh，第38行按照注释修改

注意:你在环境变量中填写的cookie不能使用换行隔开，必须要用&或者一个变量一个cookie


# 结尾

本文部分内容借鉴于其他作者旧版本教程，在此表示感谢。
由于时间过久遗失原文链接，如有作者看到请联系我添加参考出处链接

**注：本教程仅供学习交流使用,请勿用于非法交易！**
