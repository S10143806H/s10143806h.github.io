# RTLduino -- 野生Ameba開發板

:::info

關於開發板如何出現的故事。

本質上是非常社群的開發過程與結果。

:::

## 簡介

在製作Arduino相關的物聯網項目時，esp8266和esp32開發板很受大家的歡迎，它們價格低廉，易於開發，且具有連接 Wi-Fi 的能力。

但是它們也存在一些問題，最大的問題在於，它們只支持2.4GHz的 Wi-Fi 網絡，這種網絡不夠穩定，很容易受到干擾。

[爲什麽](https://www.arduino.cn/thread-101986-1-1.html) 大家自願去研究/開發這個板子，不僅因爲它原生支援雙頻 Wi-Fi 和更高級的BLE，價格低廉，且可以用Arduino開發. 

![RTLduino](https://i.imgur.com/Z0jngJO.png =200x180)

一塊約五美金，購買 [平臺](https://www.aliexpress.com/item/1005001768102716.html), 并且對 arduuino 的支援度非常高。

下面是RTL8720DN和RTL8722DM的對比：[Ameba Intro.pdf](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d4f35900-2967-4128-8e8f-28381f2bd885/AmebaIntro.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210629%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210629T033530Z&X-Amz-Expires=86400&X-Amz-Signature=005ee99d6b908ed43339909f04e1a47657290a6a31f1cb1f77bf311a589270f6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22AmebaIntro.pdf%22)


## 硬體配置

![BW16](https://i.imgur.com/wYyEAJ4.png =180x110)

1. IC 設計: Realtek - **RTL8720DN**
    - ARMV8M Cortex-M33 基本指令相容Cortex-M4
    - ARMV8M Cortex-M23 相容於Cortex-M0+
    - WLAN(802.11 a / b / g / n)
    - MAC
    - Bluetooth baseband 
    - RF baseband
    - *RTL8720DN vs RTL8722DM:* [Ameba Intro.pdf](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d4f35900-2967-4128-8e8f-28381f2bd885/AmebaIntro.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210629%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210629T033530Z&X-Amz-Expires=86400&X-Amz-Signature=005ee99d6b908ed43339909f04e1a47657290a6a31f1cb1f77bf311a589270f6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22AmebaIntro.pdf%22)

2. 模組: B&T（[博安通](http://www.tech-now.com/product-3.html)) - [**BW16**](https://www.seeedstudio.com/Realtek8720DN-2-4G-5G-Dual-Bands-Wireless-and-BLE5-0-Combo-Module-p-4442.html)
    
    - 5G & 2.4G Dual-bands WiFi
    - Bluetooth Low Energy (BLE) 5.0
    
3. 開發板：[AI-Thinker](http://www.ai-thinker.com/index.html) - **Rtlduirno**

## 燒錄須知

燒錄firmware須知：
接下来就要将代码上传到开发板上了，这也是这个开发板的第一个坑点：
:::danger
这个芯片上传程序的串口是LOG_TX(PA7)和LOG_RX(PA8),
而这个开发板的板载USB转串口芯片连接的是串口是:TX_0(PB1)和RX_0(PB2).
你可以使用另一个USB转串口模块来连接LOG_TX和LOG_RX串口，不过你也可以用两条线将
PA7 -- PB1 相连，
PA8 -- PB2 相连，
这样就可以利用板载的USB转串口芯片上传程序。
:::


---

# BW16 模組

## BW16 Pin Map
![BW16 Pin Map](https://i.imgur.com/Y6mDGfJ.png =600x700)

---

# 购买渠道

- [Seeed Studio](https://www.seeedstudio.com/Realtek8720DN-2-4G-5G-Dual-Bands-Wireless-and-BLE5-0-Combo-Module-p-4442.html) 上 USD 3.90 可以买到一个模组

---

# 相关资料

1. [陈亮 Instructable](https://www.instructables.com/RTL8720DN/)
2. [Arduino.cn Happyme](https://www.arduino.cn/thread-101986-1-1.html)
3. BW16 规格书 [中文](https://docs.ai-thinker.com/_media/bw16_%E8%A7%84%E6%A0%BC%E4%B9%A6.pdf)/[英文](https://files.seeedstudio.com/products/102110419/Basic%20documents/bw16_product_specification_en.pdf)
4. [BW16原理圖](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/90a215ac-8142-4afa-b4bc-ada15bc1f290/bw16_schematics-v1.0.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210629%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210629T124849Z&X-Amz-Expires=86400&X-Amz-Signature=d08950cb9664f2e4324454d47fe3fb6337528e84511809b044664b5206637eca&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22bw16_schematics-v1.0.pdf%22)
5. [BW16 AT指令手冊](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e10afc80-951a-4e12-9f18-7f13ef1cc112/rtl8720d-at-commands-v2.4.1-20190814.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210629%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210629T124847Z&X-Amz-Expires=86400&X-Amz-Signature=f82dd51345d76296844aedb0451b5597a5f08b41db01e50446f492ed86c02733&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22rtl8720d-at-commands-v2.4.1-20190814.pdf%22)
6. [BW16 連接 TCP服務器](https://zhuanlan.zhihu.com/p/281452883)
7. [RTL8720DN Datasheet](https://files.seeedstudio.com/products/102110419/Basic%20documents/00014457-UM0401-RTL872xD-Datasheet-v1.7_205016.pdf)
8. [AN0040 AmebaD Application Note](https://files.seeedstudio.com/products/102110419/Basic%20documents/00014218-AN0400-Ameba-D-Application-Note-v09_205022.pdf)
9. [RTL8720D 常見問題](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/931f04e8-0918-4d77-b25d-a772f372834b/rtl8720d-FAQ-20190604.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210629%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210629T124631Z&X-Amz-Expires=86400&X-Amz-Signature=857617a8005c83b7e5ba88afe5f5f3d83e7b3c53552d2916bd30bbdc7085c781&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22rtl8720d-FAQ-20190604.pdf%22)



---

# 故事

## 故事的起始 — 一個 Github 的 issue

今年一月6號，有一個叫做 happyme531 的 Github 用戶，在瑞昱官方維護的 ambd_micropython repository 裏面創建了一個 issue，名字叫"Support for BW16 module dev board (RTL8720DN)"

[Support for BW16 module dev board (RTL8720DN) · Issue #2 · ambiot/ambd_micropython](https://github.com/ambiot/ambd_micropython/issues/2)

有趣的是，這個用戶不僅提出了一塊開源社區開發團隊根本沒有聽説過的開發板，還給我們提供了一系列勁爆的信息，

:::success
1. 它的價錢—只要$5！
2. 它已經可以使用 Arduino IDE 進行開發了
3. 這個開發板的出處（生產商）
:::

雖然最終沒能成功解決這個 issue，但是這個用戶的提問反應了這塊板子在 maker 圈應該是已經有所流通并且有人真的很喜歡它，不惜無償爲它配置開發環境和製作更多的開發案例。

## 故事的承接 — 尋找alpha開發者

爲了進一步瞭解開發 BW16 的開發者，從而找到 Alpha 開發者，也就是 BW16 能夠進入 maker 圈的始作俑者，依靠這個 Github 用戶留下的信息（他的個人介紹：“A Chinese student and programming beginner.” 并且他使用 QQ），順藤摸瓜，終於在 Arduino 中文社區裏面找到了蛛絲馬跡

[支持双频WiFi和蓝牙ble5.0的Arduino开发板:Ameba RTL8720DN rtlduino-Arduino中文社区 - Powered by Discuz!](https://www.arduino.cn/forum.php?mod=viewthread&tid=101986&extra=&highlight=RTL8720DN&page=1)

原來有一個名叫 a2302004040 的用戶在這個論壇上 post 了關於如何修改 Ameba D arduino 的官方下載包中的文件，來使其與 RTL8720DN 兼容的教程文章，内容非常詳細，細節也處理的恰到好處，不會讓人覺得太麻煩，也不會覺得沒有挑戰性，所以基本上任何有一些 arduino 開發經驗的人以及對這個開發板有興趣的人，都會對這個教程躍躍欲試。

## 故事的轉折 — 如何購買？官方支援？

從上面的 post 裏面可以找到作者購買的鏈接是在淘寶上面的，經過多次嘗試，才終於找到了購買的鏈接

[博安通RTL8720DN 双频WiFi+低功耗蓝牙5.0模块 板载/外接天线BW16-淘宝网](https://item.taobao.com/item.htm?spm=a1z0d.6639537.1997196601.126.23357484xJfLA5&id=610183312653)

但是這個產品并沒有面向海外的界面和寄送方式，該怎麽購買呢？做了一些調查后發現，原來在淘寶上出售這個開發板的是大陸的 AI-Thinker 安信可公司，他們的官網上面有購買樣品的鏈接，正好連去 alibaba，在跟 alibaba 的安信可客服再三確認之後，發現他們確實是可以提供 BW16 的開發板的，而且價格和淘寶上面幾乎一致 — 5美刀一片，模塊則是 3.5美刀。 也是毫不猶豫的購買了幾片，貨運速度很快，幾天就送到了，拿到手之後第一時間使用已經修改好的arduino IDE 來給 BW16 燒錄固件， 成功！ 并且驗證了它確實是支援雙頻 wifi 和 BLE 5.0 的，一下子這個開發板的價值就高了很多，因爲真的很便宜，功能也非常强大，在同樣 specs 的開發板裏面粗略地看了一下，完全沒有對手！

下一步，問題就來了，爲什麽這麽適合開源社群的板子，官方沒有支援？ 詢問的過程十分曲折，但是得到的回復是非常堅定的 — 那就是這個板子的 feature 沒有官方支援的 RTL8722 那麽多，且硬件設計不是官方負責的，因此很不可控，不好維護。

既然官方不維護，那麽接下來怎麽辦呢？

## 故事的結尾1 — 使用者終成貢獻者

答案就是開源社區用戶的共同命運 — 使用者終將成爲貢獻者。 自古有來無往非禮也，既然被人投之以桃，自然要報之以梨。 

在 Github 上搜尋了一遍后發現，關於 RTL8720DN 的 Github repo 和有價值的資源其實是有不少的，最有價值的比如，

1. 安信可的 RTL8720 的 SDK （理論上應該是沒有開源的）

[luanxg/RTL8720-SDK](https://github.com/luanxg/RTL8720-SDK)

2. mikey60 的 Arduino 開發環境修改文件和數量很可觀的實例

[mikey60/BW16-RTL8720DN-Module-Arduino](https://github.com/mikey60/BW16-RTL8720DN-Module-Arduino)

在看到這麽多人自發的維護這個開發板后，被感動到也決定加入到開源開發的隊伍中去，用愛發電~ 因此自行創建了一個 RTL8720DN 專用的 Arduino board manager 下載鏈接，幫助開發者，一鍵下載安裝所有需要的開發環境和工具，再也不用手動尋找和修改文件了

[xidameng/RTL8720DN_BW16_Arduino](https://github.com/xidameng/RTL8720DN_BW16_Arduino)

## 故事的結尾2 - Github Contribution

“happyme” 用戶上交了一個pull request，把他自己測試維護的BW16的arduino開發環境提交給了官方ameba arduino倉庫，官方已經重視，并且承諾會在後續的開發中合并這次用戶的提交