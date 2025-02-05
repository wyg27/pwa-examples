# PWA Examples

Examples for progressive web apps.

In this repo, we currently have:

* [CycleTracker](cycletracker): A basic app for tracking menstrual cycles. The app's HTML includes a form to add a period cycle start and end dates. The JavaScript app functionality sorts the dates and saves thems to local storage. It also displays the dates retrieved from local storage below the form. The app includes a manifest file with three icons, color scheme, etc. The app also includes a service worker to handle asset caching.

* [a2hs](a2hs): An example set up to show how Add to home screen (A2HS) works. [See it live here](https://mdn.github.io/pwa-examples/a2hs/). This includes an icon and [manifest file](a2hs/manifest.webmanifest) for allowing the app to be added to home screen, and a [simple service worker](a2hs/sw.js) for making the site work offline.

* [js13kpwa](js13kpwa): A list of A-Frame entries submitted to the js13kGames 2017 competition, used as an example for the MDN articles about Progressive Web Apps. The js13kPWA have the App Shell structure, works offline with the Service Worker, is installable thanks to the Manifest file and Add to Homescreen feature, and is re-engageable by using Notifications and Push. [See it live here](https://mdn.github.io/pwa-examples/js13kpwa/).

## MDN Tutorial

https://developer.mozilla.org/zh-CN/docs/Web/Progressive_web_apps/Tutorials/CycleTracker

## 如何在 Windows 下设置本地开发环境

首先，安装 `ws` 这个服务器。运行 `npm install ws`。

然后需要解决自签名证书的问题，否则即便通过命令 `ws --https` 运行了服务器，浏览器也会认为 `https://127.0.0.1:8000` 这样的 URL 不安全。生成自签名证书最简便的办法是利用 [https://github.com/FiloSottile/mkcert/releases/tag/v1.4.4](https://github.com/FiloSottile/mkcert) 这个 Go 编写的工具，直接下载它的二进制版本。关于该工具的使用可以参考教程 [本地https快速解决方案——mkcert](https://blog.dteam.top/posts/2019-04/%E6%9C%AC%E5%9C%B0https%E5%BF%AB%E9%80%9F%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88mkcert.html)，以下仅提供一个简单的使用步骤。

Step 1：执行 `.\mkcert-v1.4.4-windows-amd64.exe -install`，这一步是在你的系统中导入一个受信任的根证书发行机构（名字是“mkert ***”）。这样，由它生成的自签名证书就会被浏览器信任了。

Step 2：执行 `.\mkcert-v1.4.4-windows-amd64.exe localhost 127.0.0.1`，这会生成自签名证书和 key，名字分别是“localhost+1.pem”和“localhost+1-key.pem”。

证书就绪之后，在代码的根目录下执行 `ws --https --cert localhost+1.pem --key localhost+1-key.pem` 就可以了。如果不出意外，访问 `https://127.0.0.1:8000` 时就会看到它被浏览器信任了。
