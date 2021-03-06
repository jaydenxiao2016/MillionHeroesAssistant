# MillionHeroesAssistant

# 百万英雄/冲顶大会/芝士超人 辅助小工具<br/>(限安卓手机，IOS用户可参考模拟器方法)<br/>

## 更新内容
新增assistant_test.py，对选项检索出次数，推荐出可能答案

## 运行环境
* Python 3.6(目前已知3.6.4有些问题，建议用3.6.3及以下版本)<br/>
* android-platform-tools（访问[google](https://developer.android.google.cn/studio/releases/platform-tools.html)下载，默认 mac，windows， linux 均支持，同时将adb工具所在路径添加到环境变量—系统变量-Path下）<br/>
* ~~baidu-aip（百度的SDK，可以直接pip安装，也可以到https://ai.baidu.com/sdk 去下载安装）<br/>~~
* 新增requirements.txt，可以pip install -r requirements.txt进行依赖环境的安装，囊括所有lib


## 基本思路
通过adb对安卓手机截图，再将问题区域裁剪出来调用百度的ocr识别出文本<br/>
然后调用百度搜索（尽可能去除百度软广的情况下，显示前两个答案）

## 百度ocr
百度ocr：https://cloud.baidu.com/product/ocr.html<br/>
注册登录后进入右上角控制台，再左侧找到文字识别，创建一个应用，默认设置即可。<br/>
重点来了，找到AppID、API Key、Secret Key，后面需要在程序中填入自己的ID和密钥。<br/>
![image](https://github.com/yyzhou94/MillionHeroesAssistant/blob/master/4.png?raw=true)
当然，也有好多用汉王ocr的，但是百度的优势就在于免费，每天500次识别次数！！！<br/>
个人认为绝对够用了，至于效果嘛，我测试到现在目前来看还比较可靠。<br/>

## 部署与使用(安卓真机)
1. 手机打开开发者模式和USB调试，连接电脑，信任后，使用`adb devices`来检查是否有自己的设备，确认已经连接
2. 在assistant.py或assistant_test.py中填入自己的百度ocr的AppID、API Key、Secret Key
3. 打开手机上的答题app，等待有题目的时候运行`python assistant.py`或`python assistant_test.py`
4. 等待几秒后，将根据识别出的问题进行百度搜索，并返回两个搜索结果或推荐答案
5. 答案仅供参考，辅助锦上添花，奖金不论多少，知识才是无价之宝

## 部署与使用(模拟器方法)
1. 使用夜神安卓模拟器（其他模拟器是否可行暂无测试），在设置中打开开发者模式和USB调试（具体方法可百度），同时将分辨率修改为手机模式1080X1920(默认平板模式)
2. cd到夜神模拟器所在目录后，使用`adb connect 127.0.0.1:62001`，连接上模拟器
3. 在assistant.py或assistant_test.py中填入自己的百度ocr的AppID、API Key、Secret Key
4. 打开模拟器上的答题app，等待有题目的时候运行`python assistant.py`或`python assistant_test.py`
5. 等待几秒后，将根据识别出的问题进行百度搜索，并返回两个搜索结果或推荐答案


## 测试结果
屏幕所示问题如下：<br/>
![image](https://github.com/yyzhou94/MillionHeroesAssistant/blob/master/screenshot.png?raw=true)<br/>
截取部分如下：<br/>
![image](https://github.com/yyzhou94/MillionHeroesAssistant/blob/master/crop_test1.png?raw=true)<br/>
返回答案：<br/>
![image](https://github.com/yyzhou94/MillionHeroesAssistant/blob/master/1.PNG?raw=true)<br/>
新版返回答案：<br/>
![image](https://github.com/yyzhou94/MillionHeroesAssistant/blob/master/3.png?raw=true)<br/>
## 分支说明

- master: 主要是调用百度的SDK
- api: 用百度的api接口进行POST（原谅我固执的又做一个没什么区别的分支，可能是无聊吧）

## 参考项目
结合了两位大神的项目，尽量简化源码。<br/>
但是对于效果上想要进一步提高，目前有些思路但是还没有考虑清楚如何实现<br/>
- [wuditken/MillionHeroes](https://github.com/wuditken/MillionHeroes)
- [smileboywtu/MillionHeroAssistant](https://github.com/smileboywtu/MillionHeroAssistant)
