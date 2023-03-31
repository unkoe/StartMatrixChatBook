# 快速开始

在看本文前，你可能需要看一下 Matrix 关于 `Homeserver` 的 [介绍](introduction.html)。
当然，如果你只是服务器的一位用户，你也完全可以不用去了解这些细节，只需要知道你在使用一台主服务器聊天，
需要设置它即可。

了解了 Matrix 和其它聊天软件的不同之处后，我们就可以开始使用了。

## 网页版

大部分 Matrix 服务器均提供了网页版客户端。它们的网址一般形如`https://element.nibbana.jp/`，这种情况下可以直接使用网页版。

## 客户端

Matrix 的客户端实现有很多，其中 `Element` 是 [官方](https://element.io/) 提供的客户端实现。
当然，我们也可以使用 [其它](https://matrix.org/docs/projects/try-matrix-now/#clients) 开源实现，
它们基本都涵盖了所有平台(Linux/Windows/Android/Mac/Ios)，如果你遇到打不开的情况，可能需要一些翻墙技巧的帮助。

👇**下面将提供 Element⚡ 使用步骤** 👇👇

### Element Windows客户端

由于笔者使用的是 `Windows` 和 `Android` 平台， 所以无法演示 `Mac` 和 `iOS` 的客户端。但是理论上它们的交互甚至UI都是一致的。
你可以参考下面演示 `Element for Windows` 的交互逻辑，完成自己的第一次 Homeserver 配置，注册、登录等操作。

#### 安装

> 注意：你可能需要先 [配置](ss_proxy.html) Shadowsocks 代理 再继续下面的操作。

这个章节使用的是 [Windows 安装包](https://packages.riot.im/desktop/install/win32/x64/Element%20Setup.exe) ，
你也许需要其它的 [安装包](https://element.io/) ，安装步骤非常简单，双击它就会自动安装到用户应用路径: 
```text
C:\Users\%USERPROFILE%\AppData\Local\element-desktop
```

#### 不使用代理访问 Matrix

[参考资料](https://github.com/vector-im/element-web/blob/develop/docs/config.md#homeserver-configuration)

选择一个可以直连的 Matrix Homeserver，记录主域名（以下表示为`EXAMPLE.com`）（假如你注册了一个名为user的账户，你的Matrix ID（见下）应显示为@user:EXAMPLE.com）。

访问`https://EXAMPLE.com/.well-known/matrix/client`，复制所有内容（包括开头和结尾的大括号）。

运行一次Element，出现错误界面后退出。

在数据目录内新建文件`config.json`，编辑，更改为以下内容：

```text
{
    "default_server_config": 在这里按下 Ctrl+V 粘贴
}
```

最终，你得到的`config.json`应当形如下面的示例：

```json
{
    "default_server_config": {
        "m.homeserver": {
            "base_url": "https://EXAMPLE.com"
        }
    }
}
```

或者

```json
{ 
  "m.homeserver": {
    "base_url": "https://matrix.EXAMPLE.com"
  },
  "m.identity_server": {
    "base_url": "https://vector.im"
  }
}
```

数据目录位置（Windows）：
原版：`%APPDATA%\Element`（也就是`C:\Users\用户名\AppData\Roaming\Element`）
[绿色版](https://portapps.io/app/element-portable/)：安装目录下的`data`文件夹

直接打开Element，正常出现登录页面即为成功。

#### Homeserver 设置

如果你仔细看过关于 Homeserver 的 [介绍](introduction.html)，你可以发现由于 Matrix 是通过 Homeserver 维护用户和聊天室，
我们需要做的是**将这个 Homeserver 配置在应用中**，以便向目标的 Matrix Server 请求服务。

- `Homesever` 你可以理解为一个由个人运营的服务器。
- 如果你是第一次使用，需要向这个 Homeserver 进行**创建账号**。需要注意的是，Homeserver 的管理员需要开启注册配置。
- 如图，默认它是官方的 Homesever。我们将 `matrix.org` 替换成自己选择的 Homesever 即可。
- 你可以从 [这份非官方列表](https://joinmatrix.org/servers/) 中选择一个服务器使用。
- 为了避免浪费公共资源，请不要注册多个帐号而不使用。

![Element登录页](_static/element_login_page.png)

#### 储存自己的密钥

登录成功后，你需要保存自己的密钥，它是一串字符，你也可以用文本的形式保存，基本上它被命名为：
```text
security-key.txt
```
以后再登录时需要用它进行校验，或者用其它已登录的设备扫码校验，但这总归是不方便的，所有需要注意不要丢失它。

#### Matrix ID

点击头像后，你会发现自己的`Matrix ID`。它是一个唯一的身份信息，添加用户时你将用到它。

基本上，它是这样组成的：

```
@user:servername.com
@用户名:配置的servernname
```
如图：

![Matrix ID](_static/user_d.png)

#### 聊天之前

Element原生支持简体中文，可以按如下步骤激活：点击头像 -> “All settings” -> “General” -> “Language and region” -> “简体中文”。

由于使用了端对端加密，为了保证您能读取他人的消息，请在“设置” -> “安全与隐私”中开启“安全备份”（也可能显示为“Secure Backup”或“恢复已加密信息”）。

## 服务端

...