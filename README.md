# epeius
这是一个基于 CF Worker 平台的脚本，在原版的基础上修改了显示 Trojan 配置信息转换为订阅内容。使用该脚本，你可以方便地将 Trojan 配置信息使用在线配置转换到 Clash 或 Singbox 等工具中。

- **一步到位**部署视频教程：https://youtu.be/MBlAqYajVSY ***小白必看 一步到胃 最佳推荐!!!***
- **自制优选**订阅视频教程：https://youtu.be/jOhq3QpXG_I *折腾自己的专属订阅*
- **进阶使用**技巧视频教程：https://youtu.be/0Cd8uTNJj1Q *然后成为折腾的王*

Telegram交流群：[@CMLiussss](https://t.me/CMLiussss)，**感谢[Alice Networks](https://alicenetworks.net/)提供的云服务器维持[CM订阅转换服务](https://sub.fxxk.dedyn.io/)！**

# 免责声明

本免责声明适用于 GitHub 上的 “epeius” 项目（以下简称“该项目”），项目链接为：https://github.com/cmliu/epeius

### 用途
该项目被设计和开发仅供学习、研究和安全测试目的。它旨在为安全研究者、学术界人士和技术爱好者提供一个了解和实践网络通信技术的工具。

### 合法性
使用者在下载和使用该项目时，必须遵守当地法律和规定。使用者有责任确保他们的行为符合其所在地区的法律、规章以及其他适用的规定。

### 免责
1. 作为该项目的作者，我（以下简称“作者”）强调该项目应仅用于合法、道德和教育目的。
2. 作者不鼓励、不支持也不促进任何形式的非法使用该项目。如果发现该项目被用于非法或不道德的活动，作者将强烈谴责这种行为。
3. 作者对任何人或团体使用该项目进行的任何非法活动不承担责任。使用者使用该项目时产生的任何后果由使用者本人承担。
4. 作者不对使用该项目可能引起的任何直接或间接损害负责。
5. 通过使用该项目，使用者表示理解并同意本免责声明的所有条款。如果使用者不同意这些条款，应立即停止使用该项目。

作者保留随时更新本免责声明的权利，且不另行通知。最新的免责声明版本将会在该项目的 GitHub 页面上发布。

## 风险提示
- 通过提交虚假的节点配置给订阅服务，避免节点配置信息泄露。
- 另外，您也可以选择自行部署 [WorkerVless2sub 订阅生成服务](https://github.com/cmliu/WorkerVless2sub)，这样既可以利用订阅生成器的便利。

## Workers 部署方法 [视频教程](https://www.youtube.com/watch?v=MBlAqYajVSY&t=169s)
1. 部署 CF Worker：
   - 在 CF Worker 控制台中创建一个新的 Worker。
   - 将 [worker.js](https://github.com/cmliu/epeius/blob/main/_worker.js) 的内容粘贴到 Worker 编辑器中。
   - 将第 3 行 `password` 修改成你自己的 **密码**

2. 添加优选线路:
   - 给 `addresses` 按格式添加优选域名/优选IP，若不带端口号 TLS默认端口为443，#号后为备注别名，例如：
     ```js
     let addresses = [
     	//当sub为空时启用本地优选域名/优选IP
     	'www.visa.com.sg#官方优选域名',
     	'www.wto.org:8443#官方优选域名',
     	'www.csgo.com:2087',
     	'icook.hk',
     ];
     ```
   - 或 给 `sub` 添加 **Trojan优选订阅生成器** 地址，例如：
     ```js
     let sub = 'trojan.fxxk.dedyn.io';
     ```

3. 访问订阅内容：
   - 访问 `https://[YOUR-WORKERS-URL]/[PASSWORD]` 即可获取订阅内容。
   - 例如 `https://vless.google.workers.dev/auto` 就是你的通用自适应订阅地址。
   - 例如 `https://vless.google.workers.dev/auto?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://vless.google.workers.dev/auto?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://vless.google.workers.dev/auto?sb` singbox订阅格式，适用singbox等。

4. 给 workers绑定 自定义域： 
   - 在 workers控制台的 `触发器`选项卡，下方点击 `添加自定义域`。
   - 填入你已转入 CF 域名解析服务的次级域名，例如:`vless.google.com`后 点击`添加自定义域`，等待证书生效即可。

## Pages 上传 部署方法
1. 部署 CF Pages：
   - 下载 [worker.zip](https://raw.githubusercontent.com/cmliu/epeius/main/worker.zip) 文件，并点上 Star !!!
   - 在 CF Pages 控制台中选择 `上传资产`后，为你的项目取名后点击 `创建项目`，然后上传你下载好的 [worker.zip](https://raw.githubusercontent.com/cmliu/epeius/main/worker.zip) 文件后点击 `部署站点`。
   - 部署完成后点击 `继续处理站点` 后，选择 `设置` > `环境变量` > **制作**为生产环境定义变量 > `添加变量`。
     变量名称填写**PASSWORD**，值则为你的密码，后点击 `保存`即可。
   - 返回 `部署` 选项卡，在右下角点击 `创建新部署` 后，重新上传 [worker.zip](https://raw.githubusercontent.com/cmliu/epeius/main/worker.zip) 文件后点击 `保存并部署` 即可。

2. 添加优选线路:
 - 添加变量 `ADD` 本地静态的优选线路，若不带端口号 TLS默认端口为443，#号后为备注别名，例如：
   ```
   cf.090227.xyz:443#加入我的频道t.me/CMLiussss解锁更多优选节点
   time.is#你可以只放域名 如下
   www.visa.com.sg
   skk.moe#也可以放域名带端口 如下
   www.wto.org:8443
   www.csgo.com:2087#节点名放在井号之后即可
   icook.hk#若不带端口号默认端口为443
   104.17.152.41#IP也可以
   [2606:4700:e7:25:4b9:f8f8:9bfb:774a]#IPv6也OK
   ```

3. 访问订阅内容：
   - 访问 `https://[YOUR-PAGES-URL]/[PASSWORD]` 即可获取订阅内容。
   - 例如 `https://epeius.pages.dev/auto` 就是你的通用自适应订阅地址。
   - 例如 `https://epeius.pages.dev/auto?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://epeius.pages.dev/auto?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://epeius.pages.dev/auto?sb` singbox订阅格式，适用singbox等。
   - 例如 `https://epeius.pages.dev/auto?surge` surge订阅格式，适用surge 4/5。

4. 给 Pages绑定 CNAME自定义域：
   - 在 Pages控制台的 `自定义域`选项卡，下方点击 `设置自定义域`。
   - 填入你的自定义次级域名，注意不要使用你的根域名，例如：
     您分配到的域名是 `fuck.cloudns.biz`，则添加自定义域填入 `lizi.fuck.cloudns.biz`即可；
   - 按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 `lizi`的 CNAME记录 `epeius.pages.dev` 后，点击 `激活域`即可。

## Pages GitHub 部署方法 [视频教程](https://www.youtube.com/watch?v=0Cd8uTNJj1Q&t=96s)
1. 部署 CF Pages：
   - 在 Github 上先 Fork 本项目，并点上 Star !!!
   - 在 CF Pages 控制台中选择 `连接到 Git`后，选中 `epeius`项目后点击 `开始设置`。
   - 在 `设置构建和部署`页面下方，选择 `环境变量（高级）`后并 `添加变量`，
     变量名称填写**PASSWORD**，值则为你的密码，后点击 `保存并部署`即可。

2. 添加优选线路:
 - 添加变量 `ADD` 本地静态的优选线路，若不带端口号 TLS默认端口为443，#号后为备注别名，例如：
   ```
   cf.090227.xyz:443#加入我的频道t.me/CMLiussss解锁更多优选节点
   time.is#你可以只放域名 如下
   www.visa.com.sg
   skk.moe#也可以放域名带端口 如下
   www.wto.org:8443
   www.csgo.com:2087#节点名放在井号之后即可
   icook.hk#若不带端口号默认端口为443
   104.17.152.41#IP也可以
   [2606:4700:e7:25:4b9:f8f8:9bfb:774a]#IPv6也OK
   ```

3. 访问订阅内容：
   - 访问 `https://[YOUR-PAGES-URL]/[PASSWORD]` 即可获取订阅内容。
   - 例如 `https://epeius.pages.dev/auto` 就是你的通用自适应订阅地址。
   - 例如 `https://epeius.pages.dev/auto?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://epeius.pages.dev/auto?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://epeius.pages.dev/auto?sb` singbox订阅格式，适用singbox等。
   - 例如 `https://epeius.pages.dev/auto?surge` surge订阅格式，适用surge 4/5。

4. 给 Pages绑定 CNAME自定义域：
   - 在 Pages控制台的 `自定义域`选项卡，下方点击 `设置自定义域`。
   - 填入你的自定义次级域名，注意不要使用你的根域名，例如：
     您分配到的域名是 `fuck.cloudns.biz`，则添加自定义域填入 `lizi.fuck.cloudns.biz`即可；
   - 按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 `lizi`的 CNAME记录 `epeius.pages.dev` 后，点击 `激活域`即可。
   
## 变量说明
| 变量名 | 示例 | 备注 |
|--------|---------|-----|
| PASSWORD | auto | 可以取任意值 |
| PROXYIP | proxyip.fxxk.dedyn.io | 备选作为访问CFCDN站点的代理节点(支持多ProxyIP, ProxyIP之间使用`,`或 换行 作间隔) |
| SOCKS5  | user:password@127.0.0.1:1080 | 优先作为访问CFCDN站点的SOCKS5代理 |
| ADD | www.csgo.com:2087,icook.hk | 本地优选域名/优选IP(支持多元素之间`,`或 换行 作间隔) |
| ADDAPI | [https://raw.github.../addressesapi.txt](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt) | 不解释, 懂得都懂 |
| ADDCSV | [https://raw.github.../addressescsv.csv](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressescsv.csv) | 不解释, 懂得都懂 |
| DLS | 8 | `ADDCSV`测速结果满足速度下限 | 
| TGTOKEN | 6894123456:XXXXXXXXXX0qExVsBPUhHDAbXXXXXqWXgBA | 发送TG通知的机器人token | 
| TGID | 6946912345 | 接收TG通知的账户数字ID | 
| SUB | trojan.fxxk.dedyn.io | 优选订阅生成器地址(使用订阅器将放弃`ADD`内的本地优选订阅内容) |
| SUBAPI | subapi.fxxk.dedyn.io | clash、singbox等 订阅转换后端 |
| SUBCONFIG | [https://raw.github.../ACL4SSR_Online_Mini.ini](https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini.ini) | clash、singbox等 订阅转换配置文件 |
| SUBNAME | epeius | 订阅名称 | 
| RPROXYIP | false | 设为 true 即可强制获取订阅器分配的ProxyIP(需订阅器支持)|
| URL302 | https://t.me/CMLiussss | 主页302跳转(支持多url, url之间使用`,`或 换行 作间隔, 小白别用) |
| URL | https://t.me/CMLiussss | 主页伪装(支持多url, url之间使用`,`或 换行 作间隔, 乱设容易触发反诈) |
| CFEMAIL | admin@gmail.com | CF账户邮箱(与`CFKEY`都填上后, 订阅信息将显示请求使用量, 小白别用) | 
| CFKEY | c6a944b5c956b6c18c2352880952bced8b85e | CF账户Global API Key(与`CFEMAIL`都填上后, 订阅信息将显示请求使用量, 小白别用) |

**注意: 填入`SOCKS5`后将不再启用`PROXYIP`！请二选一使用！！！**

**注意: 填入`SUB`后将不再启用`ADD*`类变量生成的订阅内容！请二选一使用！！！**

**注意: 同时填入`CFEMAIL`和`CFKEY`才会启用显示请求使用量，但是不推荐使用！没必要给一个Worker项目这么高的权限！后果自负！！！**

## 实用小技巧

**该项目部署的节点可通过节点PATH(路径)的方式，使用指定的`PROXYIP`或`SOCKS5`!!!**

- 指定 `PROXYIP` 案例
   ```url
   /proxyip=proxyip.fxxk.dedyn.io
   /?proxyip=proxyip.fxxk.dedyn.io
   /proxyip.fxxk.dedyn.io (仅限于域名开头为'proxyip.'的域名)
   ```

- 指定 `SOCKS5` 案例
   ```url
   /socks5=user:password@127.0.0.1:1080
   /?socks5=user:password@127.0.0.1:1080
   /socks://dXNlcjpwYXNzd29yZA==@127.0.0.1:1080
   /socks5://user:password@127.0.0.1:1080
   ```

## Star 星星走起
[![Stargazers over time](https://starchart.cc/cmliu/epeius.svg?variant=adaptive)](https://starchart.cc/cmliu/epeius)

# 感谢
[ca110us](https://github.com/ca110us/epeius)、[xream](https://github.com/xream)、[3Kmfi6HP](https://github.com/3Kmfi6HP/EDtunnel/tree/trojan)、[zizifn](https://github.com/zizifn/edgetunnel)、[emn178](https://github.com/emn178/js-sha256)、[ACL4SSR](https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash/config)、[SHIJS1999](https://github.com/SHIJS1999/cloudflare-worker-vless-ip)、<a href="https://alicenetworks.net/"><img src="https://alicenetworks.net/templates/lagom2/assets/img/logo/logo_big.194980063.png" width="150" height="75" alt="Alice Networks LTD"/></a>，
