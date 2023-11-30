# 阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP
> https://github.com/ImYrS/aliyun-auto-signin
> 
**文章发布时间：2023-03-14 10:12:19**


[阿里云盘免费SVIP](https://www.zhuji999.com/tag/15904)，[阿里云盘](https://www.zhuji999.com/tag/15771)SVIP目前是通过每月签到来领取的，像2023年3月来说，如果完成一个月31天签到可以领取36天的SVIP会员，也就是整月都是享受SVIP的。 前面说了需要每日签到才能领取到全月36天的SVIP会员！ 由于是每日必做的事情，有个时候经常会忘记，于是这里分享一个[阿里云](https://www.zhuji999.com/tag/1594)盘自动领SVIP的教程，是利用GitHub脚本实现阿里云盘每日自动签到领取免费SVIP！

阿里云盘是一个下载不限速度的网络存储盘，相对于百度云盘来说，阿里云盘在下载方面是不限速的，但是阿里云盘新推出不久，存在一定的功能不完善问题，但是下载速度是非常不错的。 同时目前阿里云盘有免费送SVIP活动，SVIP超级会员有分配8T存储空间、原画视频、多倍速播放、大文件上传的功能，并且是免费送SVIP，是不是有种不去领取阿里云盘SVIP感觉有点罪过的样子O(∩_∩)O哈哈~，撸免费的撸习惯了就会有这种表现吧。

关于网盘的介绍，[主机](https://www.zhuji999.com/tag/5487)玖玖有篇文章介绍了过呢常用的几个网盘：[百度网盘](https://www.zhuji999.com/tag/15770)、阿里云云盘、[蓝奏云存储](https://www.zhuji999.com/tag/15772)，并对百度网盘、阿里云云盘、蓝奏云存储各自优势做了对比，有需求网盘的可以查看下面文章：

- [建站文件存储及外链下载用哪些免费云盘好_百度网盘、阿里云盘、蓝奏云存储优势对比](https://www.zhuji999.com/15274.html)

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图](https://www.zhuji999.com/wp-content/uploads/2023/03/98cec24a09dc58e.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/98cec24a09dc58e.png)

 

**文章目录** 

[一、准备一个GitHub账号](https://www.zhuji999.com/15637.html#yi_zhun_bei_yi_geGitHub_zhang_hao)

[二、在GitHub创建一个阿里云盘自动签到项目库](https://www.zhuji999.com/15637.html#er_zaiGitHub_chuang_jian_yi_ge_a_li_yun_pan_zi_dong_qian_dao_xiang_mu_ku)

[三、获取自己阿里盘的Token](https://www.zhuji999.com/15637.html#san_huo_qu_zi_ji_a_li_pan_deToken)

[三、在GitHub创建一个Personal access tokens (classic)](https://www.zhuji999.com/15637.html#san_zaiGitHub_chuang_jian_yi_gePersonal_access_tokens_classic)

[四、在GitHub各设置aliyun-signin-action项目的](https://www.zhuji999.com/15637.html#si_zaiGitHub_ge_she_zhialiyun-signin-action_xiang_mu_de)

[五、在GitHub运行action实现自动签到](https://www.zhuji999.com/15637.html#wu_zaiGitHub_yun_xingaction_shi_xian_zi_dong_qian_dao)

### 一、准备一个GitHub账号

想利用GitHub脚本实现阿里云盘自动签到领取免费SVIP，想实现阿里云盘自动领SVIP，这里介绍的是利用GitHub自动执行脚本来实现，所以必须先准备一个GitHub账号。

- GitHub官网注册账号地址：[点击直达](https://www.zhuji999.com/goto/nv78gd)

### 二、在GitHub创建一个阿里云盘自动签到项目库

1、登录自己账号后，点击自己如下图位置，创建一个新的项目库。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图1](https://www.zhuji999.com/wp-content/uploads/2023/03/b3f6501d4e3fb9a.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/b3f6501d4e3fb9a.png)

2、如下图把项目名称命名为“aliyun-signin-action”！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图2](https://www.zhuji999.com/wp-content/uploads/2023/03/67cefa382b9dca0.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/67cefa382b9dca0.png)

3、然后如下图点击红框位置创建一个文件。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图3](https://www.zhuji999.com/wp-content/uploads/2023/03/6b2bb95eec8e401.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/6b2bb95eec8e401.png)

4、创建文件的路径及文件名设置为“.github/workflows/signin.yml”，直接复制粘贴到第一个红框位置即可。文件内容如下：

```
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
```

设置的效果如下图。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图4](https://www.zhuji999.com/wp-content/uploads/2023/03/9b77c4795e2096d.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/9b77c4795e2096d.png)

### 三、获取自己阿里盘的Token

1、如何获取自己阿里云盘的“REFRESH_TOKENS”。请[点击这里](https://www.zhuji999.com/goto/0ndcmd)来访问获取。然后如下图选择获取自己的阿里云盘的“TOKENS”！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图5](https://www.zhuji999.com/wp-content/uploads/2023/03/589d40aac0a7be4.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/589d40aac0a7be4.png)

2、点击上图的获取Token后，弹出如下图的一个二维码。请使用阿里云盘手机APP扫码提供的二维码后，再点击红框按钮即可获取Token！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图6](https://www.zhuji999.com/wp-content/uploads/2023/03/61fdb4e2d6a4d41.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/61fdb4e2d6a4d41.png)

3、如下图Token就获取成功了。请保存好自己的Token，后面需要用到。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图7](https://www.zhuji999.com/wp-content/uploads/2023/03/1e99050daea9e6a.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/1e99050daea9e6a.png)

### 三、在GitHub创建一个Personal access tokens (classic)

1、打开GitHub，然后登录自己的账号，点击自己头像位置，选择“Settings”！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图8](https://www.zhuji999.com/wp-content/uploads/2023/03/cd5b4e79b9f5e21.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/cd5b4e79b9f5e21.png)

2、然后在左侧点击“Developer settings”！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图9](https://www.zhuji999.com/wp-content/uploads/2023/03/84942bdaf956997.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/84942bdaf956997.png)

3、然后如下图选择创建Personal access tokens (classic)！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图10](https://www.zhuji999.com/wp-content/uploads/2023/03/4d424b7c8b2a3a1.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/4d424b7c8b2a3a1.png)

4、这里选择“repo”，Note自己随便填写。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图11](https://www.zhuji999.com/wp-content/uploads/2023/03/1aed682cbde88f8.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/1aed682cbde88f8.png)

5、创建成功后这个就是你的“tokens”，请记录好，只显示一次，记得保存到本地记事本，后面步骤需要用到这个。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图12](https://www.zhuji999.com/wp-content/uploads/2023/03/634741c8b0e3728.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/634741c8b0e3728.png)

### 四、在GitHub各设置aliyun-signin-action项目的

1、如下图操作，去创建Secrets！

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图13](https://www.zhuji999.com/wp-content/uploads/2023/03/1d11bf3920a883c.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/1d11bf3920a883c.png)

2、我们创建两个Secrets！

首先创建“GP_TOKEN”，输入的是Personal access tokens (classic)！如下图。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图14](https://www.zhuji999.com/wp-content/uploads/2023/03/120b5a339bdb7c4.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/120b5a339bdb7c4.png)

然后在创建阿里云的“REFRESH_TOKENS”。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图15](https://www.zhuji999.com/wp-content/uploads/2023/03/c900c61641ac9ee.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/c900c61641ac9ee.png)

两个都创建好了如下图。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图16](https://www.zhuji999.com/wp-content/uploads/2023/03/6aee2df1d064681.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/6aee2df1d064681.png)

### 五、在GitHub运行action实现自动签到

1、如下图，可以运行签到脚本了。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图17](https://www.zhuji999.com/wp-content/uploads/2023/03/333edb3f557de40.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/333edb3f557de40.png)

2、脚本虽然有报错，但是执行签到成功了。

[![阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP插图18](https://www.zhuji999.com/wp-content/uploads/2023/03/9b93f287f62f121.png)](https://www.zhuji999.com/wp-content/uploads/2023/03/9b93f287f62f121.png)

文章名称：《阿里云盘自动领SVIP教程_利用GitHub脚本实现阿里云盘自动签到领取免费SVIP》
文章链接：https://www.zhuji999.com/15637.html
