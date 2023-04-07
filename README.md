## 阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP
阿里云盘免费SVIP，阿里云盘SVIP目前是通过每月签到来领取的，像2023年3月来说，如果完成一个月31天签到可以领取36天的SVIP会员，也就是整月都是享受SVIP的。 前面说了需要每日签到才能领取到全月36天的SVIP会员！ 由于是每日必做的事情，有个时候经常会忘记，于是这里分享一个阿里云盘自动领SVIP的教程，是利用GitHub脚本实现阿里云盘每日自动签到领取免费SVIP！

阿里云盘是一个下载不限速度的网络存储盘，相对于百度云盘来说，阿里云盘在下载方面是不限速的，但是阿里云盘新推出不久，存在一定的功能不完善问题，但是下载速度是非常不错的。 同时目前阿里云盘有免费送SVIP活动，SVIP超级会员有分配8T存储空间、原画视频、多倍速播放、大文件上传的功能，并且是免费送SVIP，是不是有种不去领取阿里云盘SVIP感觉有点罪过的样子O(∩_∩)O哈哈~，撸免费的撸习惯了就会有这种表现吧。

关于网盘的介绍，主机玖玖有篇文章介绍了过呢常用的几个网盘：百度网盘、阿里云云盘、蓝奏云存储，并对百度网盘、阿里云云盘、蓝奏云存储各自优势做了对比，有需求网盘的可以查看下面文章：

建站文件存储及外链下载用哪些免费云盘好_百度网盘、阿里云盘、蓝奏云存储优势对比
阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图

 

文章目录  隐藏 
一、准备一个GitHub账号
二、在GitHub创建一个阿里云盘自动签到项目库
三、获取自己阿里盘的Token
三、在GitHub创建一个Personal access tokens (classic)
四、在GitHub各设置aliyun-signin-action项目的
五、在GitHub运行action实现自动签到
一、准备一个GitHub账号
想利用GitHub脚本实现阿里云盘自动签到领取免费SVIP，想实现阿里云盘自动领SVIP，这里介绍的是利用GitHub自动执行脚本来实现，所以必须先准备一个GitHub账号。

GitHub官网注册账号地址：点击直达
 

二、在GitHub创建一个阿里云盘自动签到项目库
1、登录自己账号后，点击自己如下图位置，创建一个新的项目库。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图1

2、如下图把项目名称命名为“aliyun-signin-action”！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图2

3、然后如下图点击红框位置创建一个文件。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图3

4、创建文件的路径及文件名设置为“.github/workflows/signin.yml”，直接复制粘贴到第一个红框位置即可。文件内容如下：

复制
name: Aliyun Signin

on:
  schedule:
   # 每天国际时间 17:20 运行一次, 中国时间 01:20
    - cron: '20 17 * * *'
  workflow_dispatch:
jobs:
  signin:
    name: Aliyun Signin
    runs-on: ubuntu-latest
    steps:
      - uses: ImYrS/aliyun-auto-signin@main
        with:
          REFRESH_TOKENS: ${{ secrets.REFRESH_TOKENS }}
          GP_TOKEN: ${{ secrets.GP_TOKEN}}
          PUSH_TYPES: 'TELEGRAM'
          TELEGRAM_BOT_TOKEN: ${{ secrets.TELEGRAM_BOT_TOKEN }}
          TELEGRAM_CHAT_ID: ${{ secrets.TELEGRAM_CHAT_ID }}
设置的效果如下图。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图4

三、获取自己阿里盘的Token
1、如何获取自己阿里云盘的“REFRESH_TOKENS”。请点击这里来访问获取。然后如下图选择获取自己的阿里云盘的“TOKENS”！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图5

2、点击上图的获取Token后，弹出如下图的一个二维码。请使用阿里云盘手机APP扫码提供的二维码后，再点击红框按钮即可获取Token！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图6

3、如下图Token就获取成功了。请保存好自己的Token，后面需要用到。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图7

三、在GitHub创建一个Personal access tokens (classic)
1、打开GitHub，然后登录自己的账号，点击自己头像位置，选择“Settings”！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图8

2、然后在左侧点击“Developer settings”！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图9

3、然后如下图选择创建Personal access tokens (classic)！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图10

4、这里选择“repo”，Note自己随便填写。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图11

5、创建成功后这个就是你的“tokens”，请记录好，只显示一次，记得保存到本地记事本，后面步骤需要用到这个。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图12

四、在GitHub各设置aliyun-signin-action项目的
1、如下图操作，去创建Secrets！

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图13

2、我们创建两个Secrets！

首先创建“GP_TOKEN”，输入的是Personal access tokens (classic)！如下图。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图14

然后在创建阿里云的“REFRESH_TOKENS”。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图15

两个都创建好了如下图。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图16

五、在GitHub运行action实现自动签到
1、如下图，可以运行签到脚本了。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图17

2、脚本虽然有报错，但是执行签到成功了。

阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图18

赞(2)
声明：
1、本博客不从事任何主机及服务器租赁业务，不参与任何交易，也绝非中介。 博客内容仅记录博主个人感兴趣的服务器测评结果及一些服务器相关的优惠活动，信息均摘自网络或来自服务商主动提供; 所以对本博客提及的内容不作直接、间接、法定、约定的保证，博客内容也不具备任何参考价值及引导作用，访问者需自行甄别。

2、访问本博客请务必遵守有关互联网的相关法律、规定与规则; 不能利用本博客所提及的内容从事任何违法、违规操作; 否则造成的一切后果由访问者自行承担。

3、未成年人及不能独立承担法律责任的个人及群体请勿访问本博客。

4、一旦您访问本博客，即表示您已经知晓并接受了以上声明通告。

文章名称：《阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP》
文章链接：https://www.zhuji999.com/15637.html
主机免费云盘利用GitHub实现阿里云盘自动免费领SVIP百度网盘蓝奏云存储阿里云阿里云盘阿里云盘免费SVIP阿里云盘自动领SVIP教程
