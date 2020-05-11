# scnu_ssp_ClockIn
今天你打卡了没？

脚本仅供学习交流，请勿用于其他用途。

另外代码细节写得不是很到位，意思到了就好。(跑

# 注意事项 必看！！！
## 提前准备
用于打卡的密码为[服务平台](https://ssp.scnu.edu.cn/)的密码。  
使用前务必要确认自己可以用浏览器在[服务平台](https://ssp.scnu.edu.cn/)右上角本地登录成功。  
**不要统一登录！不要统一登录！不要统一登录！**  
**本地登录！本地登录！本地登录！**  
**不知道密码就找回密码！不知道密码就找回密码！不知道密码就找回密码！**  
## 安卓打卡
安装[apk文件](https://github.com/wumcpq/scnu_ssp_ClockIn/raw/master/android/app-release.apk)即可进行打卡  
或者到[百度网盘提取码dggz](https://pan.baidu.com/s/1nR0FXhVCE8stEVZ_DT5zxg)进行下载
在release中可以下载idea工程源码

# 安装环境
python3
jdk

# 安卓
需要jsoup依赖  

## browser.py
`pip install selenium`

`pip install tkinter`

安装火狐浏览器或者谷歌浏览器并且下载geckodriver放入浏览器目录下
## requsets.py
`pip install tkinter`

`pip install re`

`pip install requests`

# 初始化
## browser.py
打开browser.py并修改如下内容，即打卡内容。
```python
username = '2018213xxxx'    # 学号
password = '你的密码'       # 密码
p = 'xx省'                  # 省份
location = 'xx市xx区/县'    # 地区
```
## requsets.py
打开requests.py并修改如下内容，即打卡内容。
```python
user = '2018xxxxx'         # 你的学号
password = 'password'      # 你的密码
area = 'xx省'              # 你的省份
location = 'xx市xx县'      # 详细位置
```

# 使用
## python脚本
初始化完成之后直接打开就可以愉快使用啦。  

## 安卓
填入数据即可进行打卡。  
第一次使用填入数据打卡后会保存内容，以后无需输入数据即可打卡。  
此外，apk没有做屏幕适配，测试中小米8体验良好。  
小米8实际使用效果图：  
![小米8效果图](https://github.com/wumcpq/scnu_ssp_ClockIn/raw/master/android/Snipaste_2020-05-10_18-12-27.jpg)

# 自动打卡
在windows下写一个批处理文件，将改批处理文件设置开机自启动即可每天打开电脑自动打卡。


# 懒癌版（其实需要先折腾一下）

## 需要的准备
* 一台有`python3`环境的VPS或者树莓派（或者其他一直开机运行的Linux主机）
* 依赖关系：`re`和`requests`
* 了解`crontab`和`vi/vim`的基本使用方法

## 需要修改的信息
修改requests-push.py里的如下信息
```python
username = '2018213xxxx'    # 学号
password = '你的密码'       # 密码
p = 'xx省'                  # 省份
location = 'xx市xx区/县'    # 地区

# 利用Server酱(http://sc.ftqq.com/3.version)将打卡结果推送到微信
# [YOUR_SCKEY]需要替换为你自己的SCKEY
push_url = 'http://sc.ftqq.com/[YOUR_SCKEY].send'
```
其中最后一项信息需要到[Server酱官网](http://sc.ftqq.com/3.version)，先用GitHub账号登录，再绑定微信，最后在[这里](http://sc.ftqq.com/?c=code)获取你的`SCKEY`

## 定时执行
把修改好的requests-push.py放到你的VPS或者树莓派里。然后用`crontab`设置定时任务。比如我设置为每天中午十二点自动执行：
	0 12 * * * python3 PATH_TO_YOUR_requests-push.py >/dev/null 2>&1
需要注意的是，如果你的Linux系统的时区不是东8区的话，`crontab`执行脚本的时间会与你设想的时间不一样。
