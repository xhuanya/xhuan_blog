---
title: freenom 免费域名自动续期
date: 2021-05-14 14:00
tags:
---
# freenom 域名自动续期
众所周知，Freenom是地球上唯一一个提供免费顶级域名的商家，不过需要每年续期，每次续期最多一年。但是每次要去手动续费就很麻烦，今天给大家带来一个小工具.支持自动续费，邮件通知等..
github附上[自动续期源码](https://github.com/luolongfei/freenom "自动续期源码")
<!--more--> 
实测效果
[![实测](https://s1.ax1x.com/2020/10/11/0gExiD.md.png "实测")](https://s1.ax1x.com/2020/10/11/0gExiD.md.png "实测")
# 部署流程
1.githubActions部署（推荐）
  第一步先来到项目首页 fork 一份代码到自己的仓库
[![项目首页](https://s1.ax1x.com/2020/10/11/0gE3Pe.png "项目首页")](https://s1.ax1x.com/2020/10/11/0gE3Pe.png "项目首页")
设置基础信息
[![设置界面](https://s1.ax1x.com/2020/10/11/0gEwa8.png "设置界面")](https://s1.ax1x.com/2020/10/11/0gEwa8.png "设置界面")
基础信息详细教程
[![设置界面](https://s1.ax1x.com/2020/10/11/0gEwa8.png "设置界面")](https://s1.ax1x.com/2020/10/11/0gEwa8.png "设置界面")

| 变量名 | 含义 | 默认值 | 是否必须 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| FREENOM_USERNAME | freenom 账户 | - | 是 | 只支持邮箱账户，不支持也不打算支持第三方社交账户登录 |
| FREENOM_PASSWORD | freenom 密码 | - | 是 | 某些特殊字符可能需要转义，在`Github actions`环境，请在除字母数字以外的字符前加上“\”，否则可能无法正确读取密码，此举是防止某些字符在`shell`命令行被解析，举个例子，比如我密码是`fei.,:!~@#$%^&*?233-_abcd^$$`，那么写到秘密变量时就应写为`fei\.\,\:\!\~\@\#\$\%\^\&\*\?233\-\_abcd\^\$\$`。而在普通`VPS`环境，则只用在密码中的“#”或单双引号前加“\”，请参考`.env.example`文件内的注释，应该没人会设置那么变态的密码吧 |
| MULTIPLE_ACCOUNTS | 多账户支持 | - | 否 | 多个账户和密码的格式必须是“`<账户1>@<密码1>\|<账户2>@<密码2>\|<账户3>@<密码3>`”，如果设置了多账户，上面的`FREENOM_USERNAME`和`FREENOM_PASSWORD`可不设置 |
| MAIL_USERNAME | 机器人邮箱账户 | - | 是 | 支持`Gmail`、`QQ邮箱`以及`163邮箱`，尽可能使用`163邮箱`或者`QQ邮箱`，而非之前推荐的`Gmail`。因为谷歌的安全机制，每次在新设备登录 `Gmail` 都会先被限制，需要手动解除限制才行，而`Github Actions`每次创建的虚拟环境都会分配一个新的设备`IP`，相当于每次都是从新设备登录`Gmail`，而我们不可能每次都去手动为`Gmail`解除登录限制，所以这种机制会导致无法发出通知邮件。具体的配置方法参考「 [配置发信邮箱](#--配置发信邮箱) 」 |
| MAIL_PASSWORD | 机器人邮箱密码 | - | 是 | `Gmail`填密码，`QQ邮箱`或`163邮箱`填授权码 |
| TO | 接收通知的邮箱 | - | 是 | 你自己最常用的邮箱，推荐使用`QQ邮箱`，用来接收机器人邮箱发出的域名相关邮件 |
| MAIL_ENABLE | 是否启用邮件推送功能 | true | 否 | `true`：启用<br>`false`：不启用<br>默认启用，如果设为`false`，不启用邮件推送功能，则上面的`MAIL_USERNAME`、`MAIL_PASSWORD`、`TO`变量变为非必须，可不设置 |
| TELEGRAM_CHAT_ID | 你的`chat_id` | - | 否 | 通过发送`/start`给`@userinfobot`可以获取自己的`id` |
| TELEGRAM_BOT_TOKEN | 你的`Telegram bot`的`token` | - | 否 ||
| TELEGRAM_BOT_ENABLE | 是否启用`Telegram Bot`推送功能 | false | 否 | `true`：启用<br>`false`：不启用<br>默认不启用，如果设为`true`，则必须设置上面的`TELEGRAM_CHAT_ID`和`TELEGRAM_BOT_TOKEN`变量 |
| NOTICE_FREQ | 通知频率 | 1 | 否 | `0`：仅当有续期操作的时候<br>`1`：每次执行 |
 详细教程直达[搭建详细教程](https://github.com/luolongfei/freenom/edit/master/README.md "搭建详细教程")


