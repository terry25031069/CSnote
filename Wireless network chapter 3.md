---
title: Wireless network chapter 3
---
# 3-1無線隨意網路
## 簡介
* 無線隨意網路(wireless ad hoc network):沒有固定的基礎架構，依靠成員之間自我溝通，自動組織建立，與電腦網路的差別在於無線隨意網路的成員可隨意移動而電腦網路不行。

* IEEE 802.11 中定義兩種基本服務集(Basic Service Set, BSS) 
    * 中控型基本服務集 (Infrastructure BSS) :主要由基地台(Access Point, AP) 負責同一服務區中所有的傳輸
    * 獨立型基本服務集 (Independent BSS, IBSS): 工作站 (Station, STA) 之間能彼此直接通訊，而不須透過基地台的協助。
        * 在較大型的無線隨意網路中，採用IBSS要交換資訊的雙方可能不在彼此的通訊範圍之內，需要其他工作站中繼 (Relay) 封包。 封包的傳送需要多點跳躍 (Multihop) 才能送到目的地。
        * 尋找路由路徑 (Routing path)，使中繼節點能把封包快速有效的傳往目的地，是基本且關鍵的任務。尋找路由路徑的過程，稱為路由探索 (Route discovery)。節點利用廣播 (Broadcast) 路由請求 (Route request, RREQ) 來獲得路由路徑。  節點散佈的區域廣泛，廣播訊息需要透過中繼節點重播 (Rebroadcast)，才能使所有節點得知，但因節點位置可能改變，造成多次重播，進而出現廣播風暴問題。  節點的電力透過電池來提供，省電成為了一項重要的議題。(藉由Protocol省電)

# 3-2媒體存取層
* 媒體存取層(Media Access Control, MAC):提供定址及媒體存取的控制方式，使得不同設備或網路上的節點可以在多點的網路上通訊，而不會互相衝突。 MAC提供配合特定通道存取(channel access method) 需要的協議及控制機制，因此連接在同一傳輸媒體的幾個設備可以共享其媒體。分為單一通道與多通道。
## 單一通道
### 固定式
* 傳送端要傳送資料時，需要以特定決定的順序來存取，例如 FDMA、TDBA、CDMA、Polling等
#### FDMA(Frequency Division Multiple Access)
![](https://i.imgur.com/UOWika7.png)
* 頻寬切成數等分，一個頻道給一個使用者使用，同時讓多使用者使用傳輸媒介。
#### TDMA (Time Division Multiple Access):
* 以時間排程輪流讓多個使用者使用相同頻率存取媒介
![](https://i.imgur.com/jnSreMA.png)
#### Hybrid FDMA/TDMA:
* 混合上述兩種方法，為讓傳輸效率更佳或更省電。
![](https://i.imgur.com/4kw6j6e.png)
#### CDMA(Code Division Multiple Access):
* 更有效的使用頻寬與時間，除了切割時間之外，每一組傳輸都會給予一組特定的編碼 (Code) ，要傳送的位元會先經過編碼再傳送出去，如果彼此的編碼是正交 (Orthogonal) ，即使使用相同的頻率也不會互相干擾。由於編碼與解碼會增加耗電量因此在電信網路4G後被OFDMA取代。
![](https://i.imgur.com/mMmXOUr.png)
#### Polling
* 主節點依次邀請從屬節點來傳送資料，但主節點故障時則無法運作，以及查詢從屬節點時造成延遲。
![](https://i.imgur.com/vIHg5Wa.png)
### 隨機存取式
* 傳送端傳送資料時隨時都可存取資料，例如Aloha、Slot Aloha、CSMA/CA等方式
#### Pure-Aloha
* 傳送端要傳送時即直接傳送，但若其他節點也正在傳送資料時會產生碰撞，要求傳送的節點越多效率也越低。(最大使用率18%)
![](https://i.imgur.com/r0bNZhm.png)
#### Slotted-Aloha
* 傳送端要傳送資料時每次使用一個時槽，每個傳輸點只能在一個時槽的開始處進行傳送，大大減少傳輸頻道的衝突。(最大使用率37%)
#### CSMA:(Carrier Sense Multiple Access)
* 傳輸之前會先偵測傳輸媒介，觀察是否有其他節點正在傳輸資料，若無正在傳輸的資料則直接傳送；因為會觀察媒介的情況， 避免碰撞，效率較Aloha好。
* CSMA的偵測機制分為兩種：
    * non-persistent CSMA: 當偵測到傳輸媒介 (Medium) 忙碌或發生衝突時，則停止偵測傳輸媒介，等一段時間後再偵測媒介。 
    * persistent CSMA: 當偵測到傳輸媒介忙碌或發生衝突時，會持續偵測並等待；若發現傳輸媒介閒置時 則立即傳送資料。
#### CSMA/CA:(Carrier Sense Multiple Access with Collision Avoidance
* 當要傳輸之前會先偵測傳輸媒介是否有其他節點正在傳輸資料，若無其他節點在傳輸資料，則直接傳輸資料；若有其他節點在傳輸資料，則延遲一段隨機時間在重新偵測是否有其他節點在傳輸資料。此機制為RTS-CTS握手
* 執行RTS-CTS握手 (handshake):
	* 在裝置發送封包之前，先發送一個很小的RTS (Request to Send) 封包給目的節點。
	* 等待目的節點回覆一個CTS (Clear to Send) 封包 ，才開始傳送。 確保在接下來的資料傳送過程中不會發生打擾。 
	* RTS與CTS封包大小都很小，以減少傳送開銷。
![](https://i.imgur.com/yfIrgdV.png)
## 多通道
* 為讓多通訊配對同時進行傳輸而不互相干擾而使用。
* 一個節點可用兩種方法使用多通道：
	* 一個節點使用數個無線收發器，每個收發器使用 和其他收發器不同的通道。
	* 每個節點都只使用一個無線收發器，為了使用多通道，收發器要在不同的通道之間切換。
* 在多通道的環境之下會遇到隱藏終端點(hiddenterminal problem)的問題。 
	* 假設每個節點會使用一個特定的通道一段時間，之後再切換使用另外一個通道一段時間；當節點之間沒有時間同步，則因為彼此切換通道的時間並不相同，可能錯過了一些訊息，因此有一定的機率產生碰撞。![](https://i.imgur.com/LDDImq1.png)
	* 當節點A與B已經在通道1完成了RTS 、CTS交換，開始傳輸資料，而原本在通道2的節點C切換到了通道1，因為並不知道節點B正在接收節點A的資料，因此發送了RTS，此RTS會在節 點B與資料封包發生碰撞；而在單一通道時，節點C因為能聽到節點B發出的CTS避免碰撞，而多通道時則發生碰撞，此問題為多通道的隱藏終端點問題，以下將依是否有同步來分別介紹多通道協定。 

### 多頻道協定
#### 節點同步:
##### 區分階段(Split Phase)
![](https://i.imgur.com/bB9a52E.png)
* 每個節點只有一個無線收發器，時間區分為控制階段與資料傳輸階段，控制階段時所有節點一起轉換到通道1，並在此階段交換RTS與CTS，預約接下來傳輸資料要使用的通道。在資料傳輸階段時便切換到上一階段預約的通道進行資料傳輸，接著控制階段再換回通道1進行通道預約。
##### 共同跳躍(Common Hopping):
* 在slot 1時節點都停留在通道1，接著一起換到通道2，通道3…依此類推，而slot 3時因為有兩個節點有資料要傳輸。  因此傳輸資料的節點會停留在通道3，而其他沒有要進行傳輸的節點則是繼續切換到通道4，再切換回通道1…依此類推，直到有資料要傳輸才會停止切換。
![](https://i.imgur.com/NzLiiDL.png)
#### 節點非同步:
##### DCA(Dynamic Channel Allocation)
* 每個節點兩個收發器，其中一個收發器固定在一個通道上，專門用來傳送控制封包，稱此通道為控制通道(Control channel)，而另外一個收發器則是專門用來傳輸資料封包，傳送資料封包的通道會從除了控制通道之外的其他所有可用通道之中選出。
* DCA運作過程中，每個節點會維護一個通道使用列表(Channel Usage List, CUL)，CUL記錄鄰居節點使用通道的狀況，這個節點便可利用自己的CUL，計算出一可使用通道列表 (Free Channel List, FCL)
![](https://i.imgur.com/XsqDj9r.png)
假設節點A想要傳送封包給節點C，會先檢查
節點C用來傳送資料的收發器是否閒置， 節點A自己是否有可用的通道用來與節點C通訊
節點A會由控制收發器傳送RTS給節點C，RTS封包中會包含節點A的可用通道列表，當節點C收到RTS 之後，會檢查自己的通道使用列表與節點A的可用通道列表，如果沒有可用通道，會送回CTS給節點A告訴節點A何時可以再發送一次RTS。
如果節點C發現有可用通道則會從可使用的通道中挑選一個出來，並標記在回覆給節點A的CTS中， 之後節點A的傳輸收發器會跳到該通道， 與節點C進行資料的傳送，並在控制通道發送一RES (Reservation)給節點A的鄰居，目的是讓節點A的鄰居知道節點A的通道使用狀況，而節點C的鄰居可以從節點C發出的CTS得知節點C的通道使用狀況，如下圖B便由CTS及RES得知節點A與節點C的通道使 用狀況。
![](https://i.imgur.com/l6rGiiB.png)
![](https://i.imgur.com/82PZFqt.png)
而如圖3.12中，節點B的鄰居節點A與節點C使用通道1傳送資料，而節點D的鄰居節點E與節點F使用通道2傳送資料，當節點B嘗試要與節點D溝通時，節 點D會發現兩者之間沒有其他可以使用的通道，因此回復CTS給節點B，請節點B過一段時間再嘗試。
#### 多頻道比較
![](https://i.imgur.com/zyguCFT.png)
* 由於每個節點皆有控制收發器，固定監聽控制通道 上的封包，因此多通道的隱藏終端點問題不會在 DCA中發生。

## 3-3 路由協定
* 路由協定分為:
	* 主動式路由協定 (pro-active routing protocol)  
	* 回應式路由協定(reactive routing protocol)
### 主動
![](https://i.imgur.com/glafNSN.png)
* 主動式路由方法先為網路中任意的兩節點建立路由資訊。當有新連線要建立時 (來源節點傳送封包到目的節點)，便能及時得到路由資訊，將封包送到目的地。
### 無線 
* 因無線隨意網路頻寬有限且移動性高，需將原應用在網際網路 (Internet) 上的路由方法做一些變化來適應。 
* 目前專為無線網路設計的主動式路由協議，大致分為距離向量法 (Distance vector) 與鏈結狀態 (Link state) 兩類路由方法。
#### 距離向量法 (Distance vector):
距離向量法是由相鄰的節點互相交換彼此的距離向量，經過持續的交換之後，此向量會記錄自己到網 路中所有節點的距離，將資訊散播到整個網路中，由此來計算出自己到整個網路中所有節點的最佳路由方法。 
距離向量演算法大部分使用Bellman-Ford演算法。 對於網路上每一條節點間的路徑，演算法皆會指定成本 (cost)。
節點會選擇一條總成本(經過路徑的所有成本總和)最低的路徑，用來把資料從來源節點送到目的節點 。
當某節點初次啟動時，將只知道它的鄰居節點 (直接連接到該節點的節點) 以及到該節點的成本。
這些資訊、目的地列表、每個目的地的總成本，以及到某個目的地所必須經過的下一個節點，構成路由表。每個節點定時地將目前所知，到各個目的地的成本的資訊，送給每個鄰居節點。 
鄰居節點則檢查這些資訊，並跟目前所知的資訊做比較；如果到某個目的地的成本比目前所知的低， 則將收到的資訊加入自己的路由表。
經過一段時間後，網路上得所有節點將會瞭解到所有目的地的最佳「下一個節點」與最低的總成本。 但運行Bellman-Ford演算法有可能因為網路鏈結失效，而產生短暫性或長時間的路由迴圈，距離計算會接近無窮大 (infinity) 的問題，使得路由難以收斂。

##### Destination-sequenced distance-vector (DSDV):
簡化路由協定及避免路由迴圈，其解決的方式是使 用遞增的序列編號 (Sequence number) 來標記每個 路由的更新封包，藉此避免路由迴圈。
運行DSDV的每個節點，除了為自己記錄一個遞增 的序列編號之外，還會為網路中每個已知的節點記 錄其目的地序列編號 (Destination sequence number) 。 
鄰居間彼此交換路由更新，其中含有距離向量，也 附帶相對的目的地序列編號，節點可以利用這個編 號來確定該距離資訊是否為最新的，越大的目的地 序列編號代表資訊越新，而越接近目的地節點的序 列編號會越大，DSDV以此來避免路由迴圈的出現。

#### 鏈結狀態 (Link state):
鏈結狀態法則是將每個節點的鏈結狀態 (自己能與 哪些節點連接) 散播到整個網路，因此當網路每個 節點拿到網路的拓樸後，各自會計算出到各節點的 最佳路由。

###### Optimized Link State Pouting (OLSR):
OLSR是傳統的鏈結 狀態路由協定 (如OSPF) 的最佳版本。  
使用了多重傳送點 (Multipoint relay, MPR) 的概念 ，以減少連結狀態更新在網路中傳播的數量。
![](https://i.imgur.com/nHUChJF.png)
###### 多重傳送點 (Multipoint relay, MPR):
MPR的概念是在一個節點的1-hop鄰居之中尋找一些 節點，成為一個子集合，在此子集合的節點能完全 的覆蓋2-hop的鄰居，此子集合中的點稱為MPR節點 。  
當節點要廣播封包時，只需要他的MPR節點做轉送，其他的鄰居節點收到廣播封包後則不需再轉播， 接著這些MPR節點的MPR節點再轉送，依此類推，便可以有效地降低廣播帶來的負擔。 
 OLSR只允許被選為MPR的節點產生鏈結狀態更新 封包，只有通往MPR節點的邊被記錄，因此當密度 較高時，更新封包的長度能有效減少。

回應式路由策略與主動式路由策略的概念不同，在回應式路由的策略中，節點只會尋找和維護有需要的路由。  
主動式路由策略中，所有的路由資訊都必需維護， 無論路徑是否會被使用；而回應式路由策略的優點 是只會尋找和維護有需要的路由，不理會不需要的路由，因而省下了這些成本。
回應式路由較適合網路流量偶然發生、只涉及少數的節點且流量大的情況。 
缺點則是首次溝通時須耗費較多的時間尋找路徑，因此封包會有較多延遲。


##### Dynamic Source Routing (DSR):

來源路由 (Source routing) 為DSR的基本路由策略，來源路由的方法是: 

每個封包的完整路由在來源節點便已經決定，並且存放在該節點中。 
路由路經的資訊附在封包的表頭(Header)中，中 繼的節點會按照該資訊，依序地往目的節點轉送 。

當一節點打算送出封包，但其路由的表格中並沒有到該目的節點的資訊時，則該節點會啟動路由探索 (Route discovery) 程序，來找尋到目的地節點的路由路徑。 
來源節點發出路由請求 (Route request, RREQ) 封包以啟動路由探索程序。 
當某一中繼節點收到RREQ封包時，它首先會判 斷是否廣播過該RREQ封包，如果是，則丟棄此 RREQ封包；如果沒有，則會更新此RREQ封包內 部的資訊，並且繼續廣播此RREQ封包。
![](https://i.imgur.com/bZqWVsO.png)
目的地節點回覆一路由回應 (Route Reply, RREP) 封包返回到啟動路由探索程序的來源節點 。 

RREP利用來源路由的策略來傳送，即RREP封包中包含有回送路徑中各個中繼節點的資訊，這些 資訊記錄在封包的表頭中，而RREP封包會依照著這些資訊送回來源節點，當來源節點收到 RREP封包後，則開始傳送資料封包。

當連結發生失敗時(發送封包到下一中繼節點失敗 )，則會產生路由錯誤 (Route Error, RERR) 封包， 送回並告知來源節點，沿途的節點會把該路由資訊清除，而當來源節點收到RERR之後，會重新啟動路由探索程序來尋找新的路徑以替代原本的路徑。 
來源節點可以收集許多條到達目的地節點的路徑 ，因此萬一原本的路徑失敗時，能夠快速使用其他的路徑代替，而不需要啟動路由探索，但路由緩衝也有可能造成路由資訊過期的現象，使用這些舊的路由會造成網路頻寬的浪費以及封包被丟棄的情況。 

圖3.14為DSR的路徑探索的例子，來源節點N1共 找到2條不同的路徑到達目的地節點N8，分別為 N1-N2-N5-N8、N1-N3-N4-N7-N8
![](https://i.imgur.com/ZBWFlPj.png)
##### Ad hoc On-Demand Distance Vector Routing (AODV):

AODV使用類似於DSR的路由探索方式來尋找路徑 ，但維護路由資訊的機制與DSR全然不同。  

AODV採用傳統的路由表格，即一個目的地一個欄位，記錄其該送往的下一個節點。因為並非使用來源路由的機制，AODV完全依靠路由表格把封包送往目的地。  
依之前收到RREQ時建立的反向路徑 (Reverse path) 的資訊，將RREP封包送回到來源節點，該反向路徑同樣記錄在路由表格中。  
與DSDV相同，AODV使用目的地序列編號來避免路由迴圈，而該序列編號會附帶在所有的路由封包中。

由於AODV與DSR不同，它沒有來源路由與竊聽的機制，使AODV能收集到的僅為數量有限的路由資訊，不像DSR有豐資訊富，但因為每筆路由資訊皆附帶有一序列編號，只有較新的資訊會被採納，舊的資訊會被捨棄，甚至還使用了計時器 (Timer) 的機制，當舊的路由資訊在計時器過時之後，便會自動刪除以確保路由資訊是足夠新的，因此能解決路由過期的問題。

##### Temporally Ordered Routing Algorithm (TORA):

TORA是另一回應式路由協定，它的路由探索程序 能計算出多條無迴圈的路徑通往目的地，構成一個 以目的地為導向的有向無迴圈圖 (Destinationoriented Directed Acyclic Graph, DAG)。  
無線隨意網路可視為一個無向圖 (Undirected Graph) 。  

TORA則把每個邊視為有方向的。

對於某一目的地來說，每個節點會記錄其到該目的地節點的距離，或稱為權重值，目的地節點權重值為0，離目的地越遠的節點其權重值越高，再以類似水往低處流的概念，將封包由權重值高的節點導向 權重值低的節點。 

而其權重值建立的過程是利用詢問/更新 (Query/Update) 的機制，當一節點嘗試要送出封包 時，會先發出詢問封包，該封包會廣播到整個網路 ，直到到達目的地節點或知道目的地節點的路由為止。

混合式路由:

路由協定效率中，路由封包所花費的額外負擔，往 往取決於流量密度 (Traffic diversity) 的影響。 
流量密度是用來評估網路中流量分布的情形。  
低流量密度表示大部分的流量集中在少數節點之間，即只有少量的來源與目的地之間配對進行溝通， 例如移動用戶想要連接至網際網路，則大部分的流量皆會集中在網際網路閘道(Gateway) 中。  
高流量密度則表示流量平均散佈到整個網路的每個節點，幾乎任兩節點都會產生溝通。

位置輔助路由協定:

位置輔助路由協定是假設某些節點或全部的節點知 道自己的位置，像是全球定位系統 (GPS) 或其他間接定位的方法，每個節點再與鄰居交換封包便能得知鄰居的地理位置，而封包的目的地位置則透過位置諮詢服務 (Location service) 查詢後得之，藉此來輔助路由的建立

當節點要送出一封包時，它利用目的地的位置，找出最接近目的地的鄰居，再轉送封包到該鄰居去， 一直重複此步驟直到到達目的地為止，此方法為貪婪轉送 (Greedy forward)，但此策略有可能因前方沒有節點可以轉送封包，使封包停滯不前，導致傳送不到目的地。

##### Location-Aided Routing (LAR):
![](https://i.imgur.com/XITGr5k.png)
假設每個節點都知道自己的位置，因此不需要任何 位置諮詢服務來查詢其他節點的位置，並依靠預先的路由探索程序做區域性的廣播來得之目的地位置 。  

與目的地的位置可計算出彼此的距離，得到距離後 再廣播路由請求封包，鄰居會比較自己到目的地的 位置是否較來源節點近，較近則轉送此路由請求，較遠則捨棄此請求，依此原則將路由請求一直送往目的地節點，因具有一定的方向性，因此能大幅減 少路由探索的額外負擔。  

此方法是在路由探索時使用，在傳送一般資料封包 時則是依照探索得到的路由傳遞。

##### 廣播風暴 （broadcast storm): 

在無線隨意網路中，節點可使用氾濫式 (Flooding) 傳輸讓網路上所有節點皆能收到廣播訊息，也就是當節點收到新的廣播封包時，便會做一次重播 (Rebroadcast) 。  

* 由於每個節點之間訊號範圍可能會有重疊的區域，造成:
	* 冗餘傳輸
	* 媒介競爭

##### Serious Redundancy
![](https://i.imgur.com/7Lc67zg.png)
冗餘重播 (Redundant rebroadcast)  
當節點決定重播一個廣播訊息時，若是其所有的鄰居皆已擁有此訊息，則廣播此封包只是浪費了網路的資源。  
因為網路中的相鄰節點一定會有重疊的區域，若是被越多的節點範圍重疊，則會收到越多相同的封包 ，而造成了浪費，因此在越密集的網路之中，使用氾濫式傳輸相當的浪費資源。

###### 封包碰撞 (Packet collision)  
因為廣播封包時不需使用隨機後退機制，因此當鄰居接收到廣播封包時，便會直接重播此訊息，因此封包之間的碰撞將更容易發生。  
廣播封包也沒有RTS/CTS的事先告知交換機制，因此碰撞後會造成封包遺失的問題。
此外，因為無線隨意網路沒有碰撞檢查的機制，當某重播封包被碰撞，即使只有第一位元受到影響， 此節點還是會將封包傳輸完畢，而這個損壞的封包可能會再與其他封包產生碰撞，因此而影響整個網路的資源。

## 3-4: 電源管理
由於行動裝置一般的電源都由電池來提供電力，在無線隨意網路下，如何達到有效率的省電是一項重要的議題，目前已有許多相關研究提出了解決方 案。  
在IEEE 802.11便提供了幾種不同的電源管理模式，第一種是主動模式 (Active Mode)。
第二種模式稱為省電模式 (Power Saving Mode)，相較於第一種模式，如果終端設備的電力來源基礎是蓄電池，為了儘可能讓設備在移動時能使用久一點，IEEE 802.11就設計出一種機制，可以定期切換至打盹 (dozing) 的狀態，以節約電力消耗。

集中式協調者工作站隔著一段固定的時間定時發出 beacon，這段時期便稱為一個beacon間隔 (beacon interval)，在每個週期的起點會傳送一個Beacon訊框，訊框中包含了一組名為traffic indication map (TIM) 的資訊。
ad hoc模式下沒有集中式協調者，因此在分散式的運作下 ， 將 beacon 區間區分為 ATIM (Announcement Traffic Indication Messages) 視窗 (window) 與競爭視窗，所有休眠的工作站，會約定在ATIM視窗內都要醒來。
電力控制 (Power Control) 
![](https://i.imgur.com/4AV2Yu9.png)
電力控制 (Power Control) 

除了讓工作站休眠之外，調整發送訊號時所用的電力是另一種節省能量的技術，除了省電之外，減少訊號之間互相干擾也是電力控制的效果，進而提高無線通道使用率 (Channel utilization)。 
在整合電力控制方案於MAC層方面，再傳送RTS、 CTS、DATA和ACK訊框時會使用不同大小的電力去傳送。

BASIC協定：
在此協定中，假設一傳送站T使用最大傳輸電力傳送RTS給接收站R，接著R也會用最大傳輸電力回CTS給T，而T可根據CTS得知傳送DATA所需的最小電力，並使用此電力傳送DATA給R；同理，R也可依據RTS得知傳送ACK訊框所需的最小電力。

結合忙碌訊息 (Busy Tones) 的電力控制協定。
此套程序除了電力控制、RTS-CTS交換程序之外，還利用了忙碌訊息。 
此協定利用了RTS-CTS交換來推算出兩工作站之間的相對距離，決定傳輸DATA時所需的最小電量。 
而忙碌訊息則是被使用來避免封包碰撞，讓附近的工作站不會因為不知道之前進行的RTS-CTS交 換，而影響到進行中的資料傳輸。

首先會將通道區分成兩個子通道 (sub-channel)，資料通道 (Data channel) 和控制通道 (Control channel)，RTS-CTS交換會在控制通道中進行。 
忙碌訊息將會占據兩個不同的狹小頻帶，分別稱為Transmit busy tones (BTt) 和Receive busy tones (BTr)，如圖所示。 
![](https://i.imgur.com/Nx6WJu6.png)
BTt的功能是工作站用來通知鄰居它正在傳送資料。  
BTr則是通知鄰居它正在接收資料。 
在工作站開始傳送DATA時會開啟BTt 。  
接收端工作站在回覆CTS時會啟動BTr。 
當有工作站想要傳送RTS時須先觀察附近是否有 BTr，若有，則不能發出訊框。 
當想回覆一個CTS時須先觀察是否有BTt，若有， 則不能回覆CTS。
![](https://i.imgur.com/aBTbSQ1.png)
# 補充
![](https://i.imgur.com/sB002wb.png)
![](https://i.imgur.com/xv739dw.png)
## Access Point Roles  

* Access points within a mesh network operate in one of the following two ways:  
    * Root access point (RAP)  
    * Mesh access point (MAP)  
* The Cisco 1130 and 1240 are equipped with the following two simultaneously operating radios:
    * 2.4-GHz radio used for client access  
    * 5-GHz radio used for data backhaul 

Cisco Mesh Access Points  

Mesh networking employs Cisco 1520 Series outdoor mesh access points and Cisco 1130 and 1240 Series indoor mesh access points  
along with the Cisco wireless LAN controller, and Cisco Wireless Control System (WCS) to provide scalable, central management, and mobility between indoor and outdoor deployments.  
Control and Provisioning of Wireless Access Points (CAPWAP) protocol manages the connection of mesh access points to the network.

Abstract  
The Control And Provisioning of Wireless Access Points (CAPWAP) protocol is under definition within the IETF to enable an Access Controller (AC) to manage a collection of Wireless Termination Points (WTPs). 
 CAPWAP aims at simplifying the deployment and control of large scale, possibly heterogeneous, wireless networks.  
This work presents the first open source implementation of the CAPWAP protocol along with early experimental results aiming at the assessment of its reliability and performances.


These issues forced network vendors to propose proprietary centralized solutions aiming at simplifying functionalities commonly requested by network administrators.  
All proposed solutions share two common elements: (i) they split functionalities that APs provide and (ii) they add more centralized functions for the monitoring and the remote control of the network.
Splitting functionalities of APs allows the implementation of more flexible network infrastructures.  
It allows centralizing the management of critical functions like channel selection, authentication and encryption.  
Whereas, leaving in the APs time-critical functions, like beacon generation and frames’ acknowledgment, avoids the introduction of expensive components, like high performance interconnections, making proposed solutions competitive on the market.  
Moreover, the introduction of additional proprietary functions may further increase the level of flexibility in configuring and managing the network.
An Internet Engineering Task Force (IETF) Working Group, named Control and Provisioning of Wireless Access Points (CAPWAP), started its activity with the goal of defining standard solutions.  
The CAPWAP WG focused on problems like configuration, monitoring, control and management of large scale deployments of wireless networks in general.  
The WG is currently working on the definition of a protocol, the CAPWAP protocol, capable of providing interoperability among devices supporting these functions.
The CAPWAP protocol  
The increasing diffusion of Wireless Local Area Networks (WLANs), characterized by a number of simple Access Points, named in the following Wireless Termination Points (WTPs), and having a single point of control, called Access Controller (AC).  
The Control And Provisioning of Wireless Access Points (CAPWAP) is a recent effort of IETF aiming at defining an interoperable protocol, enabling an AC to manage and control a collection of possibly heterogeneous WTPs. 
The goals of CAPWAP 
1. Centralize authentication and policy enforcement functions for a wireless network; 
2. Move processing away from the WTPs, leaving there only time critical functions and 
3. Provide a generic encapsulation and transport mechanism. 

CAPWAP control and data messages are sent using UDP, over separate UDP ports, and secured using Datagram Transport Layer Security (DTLS).

CAPWAP data/control messages  
Two types of payload may be managed by this transport protocol: CAPWAP data messages and CAPWAP control messages.  
CAPWAP data messages encapsulate wireless frames forwarded by the WTP to the AC or by the AC to the WTP.  
CAPWAP control messages are CAPWAP management, control or monitoring messages exchanged among AC and WTPs.

Discovery  
CAPWAP also defines a discovery protocol for the automatic association of WTPs to the AC.  
As soon as the WTP is turned on, it sends a Discovery Request message (Discovery phase).  
Any AC receiving this request responds with a Discovery Response message.  
The WTP selects the AC, if any responded, with which it wants to interact and it establishes a DTLS session with it.  
Once the DTLS session has been established, both devices exchange their configurations and capabilities.  
The WTP is then ready to send and receive CAPWAP messages to/from the AC (Run phase). 

2.1. Binding definitions and IEEE 802.11  
The implementation of CAPWAP for a specific wireless technology is called ”binding”.  
Devises two operational architectures: Split MAC (SM) and Local MAC (LM).  
The difference between the two architectures is based on where specific functionalities are implemented: in the WTP, in the AC or in both.  
Table 1 summarizes where specific functionalities may be implemented in the two cases.
![](https://i.imgur.com/sz6bpFM.png)
Split MAC architecture  
In both Split MAC and Local MAC architectures the CAPWAP functionalities reside on the AC.  
In a Split MAC architecture, the Distribution and the Integration services reside on the AC, whereas in a Local MAC architecture, they reside on the WTP.  
The Distribution service enables the Medium Access Control (MAC) layer to transport MAC service data units (MSDUs) between stations, when those stations cannot communicate directly over a single instance of the wireless medium (WM). 

Split MAC  
The Integration service enables the delivery of MSDUs between IEEE 802.11 and non-IEEE 802.11 devices. 
 In Split MAC architectures, hence, all user data are tunneled between the AC and the WTP, while in Local MAC architectures not all station-generated frames are forwarded to the AC. 
In both architectures, real-time IEEE 802.11 services, including beacon generation and probe responses, are implemented on the WTP. 
Remaining management frames are supported on the AC, when Split MAC is adopted, while they are supported on the WTP. 

Association  
The AC may need to be aware of mobility events within WTPs, the WTP has to forward to the AC all the Association Request messages it receives
CAPWAP data message encapsulation  
When needed, the transport of IEEE 802.11 frames is realized using the CAPWAP data message encapsulation rules.  
IEEE 802.11 header and payload are encapsulated, while the FCS checksum is excluded.  
An optional CAPWAP header may be added. When the frame is encapsulated by the WTP, the optional header is that depicted in Fig. 1a and it gathers information on the Received Signal Strength Information (RSSI), the Signal-to-Noise-Ratio (SNR) and the data rate used by the sending station. 
![](https://i.imgur.com/0IVypFL.png)

When the frame is encapsulated by the AC, the optional header is that depicted in Fig. 1b and it informs the WTP about the WLAN ID to be used when sending the frame.
![](https://i.imgur.com/SssvB8x.png)

Conclusion  
In summary, in Local MAC mode the whole 802.11 MAC resides on the WTPs, including all the 802.11 management and control frame processing for the STAs whereas in Split MAC mode only real-time MAC functions should be managed by WTPs. 
Such distinction appears quite sharp but actually in the IEEE 802.11 specifications there is no a clear definition of which 802.11 MAC functions are considered real-time, so that each vendor may decide to use his own interpretation. 
* 感謝: 王俊霖同學提供

###### tags: `Wireless Network` `CSnote`