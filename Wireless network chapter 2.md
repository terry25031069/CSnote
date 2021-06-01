---
title: Wireless network chapter 2
---
# medium access control (MAC)
* 爭奪與衝突迴避
* Two types off access methods
    * 分散協調式功能 (Distributed Coordination Function, 簡稱 DCF )
    * 集中協調式功能 (Point Coordination Function, 簡稱 PCF )
## IEEE 802.11 Distributed Coordination Function (DCF) Channel Access
![](https://i.imgur.com/xCPQvpE.png)
* 基本存取方法，它主要是利用一種叫做載波感測多重存取及碰撞避免(Carrier-Sense Multiple Access/Collision Avoidance,簡稱 CSMA/CA) 的技術，提供行動台收送非同步資料，這種方法可用在無基礎架構 (Ad Hoc) 和具基礎建設 (Infrastructure) 的無線區域網路架構中。
    * CSMA/CA: 發現傳輸媒介由忙碌變成空閒時，先產生一段隨機延遲時間，然後才傳送訊框。**預先**避免碰撞
* 訊框間隔(Inter-Frame Space, IFS)
    * 訊框分為四種不同的優先權等級，每種優先權等級的訊框在傳送之前都必需等待一段訊框間隔(Inter-Frame Space, IFS)，才可能獲得通道的使用權
    * SIFS (Short IFS)：短訊框間隔；用來做立即的回應動作。其中要求傳送訊框 (RTS)、允許傳送訊框 (CTS)、回覆訊框(ACK) 等等，所有等候時間都是 SIFS等級。
    * PIFS (PCF IFS)：PCF 訊框間隔；在進行 PCF 免競爭式傳輸功能時，行動台傳送訊框前所必須等待的時間。
    *  DIFS (DCF IFS)：DCF 訊框間隔；在進行 DCF 競爭式傳輸功能時，行動台傳送訊框前所必須等待的時間。
    * EIFS (Extended IFS)：延長訊框間隔；行動台在進行重送訊框時所必須等待的時間。


###### tags: `Wireless Network` `CSnote`

