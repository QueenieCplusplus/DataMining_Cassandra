# DataMining_Cassandra
又稱為 C＊，是鍵值對和欄式結合的分散式料庫系統，此資料庫是使用 Java 語言。

在 DB-Engines 中，Cassandra 是 noSQL 資料庫中排名第 2 高的（僅次於 MongoDB ）。

# 起源

2007 年由臉書團隊為了解決收件箱太多資料要處理，但需要擴張的問題，從而設計讓資料得以複製與修改，且能隨時讀寫的後端資料庫系統架構，直至 2011年方才成熟。

目前貢獻的遞交者包含蘋果、LinkedIn、Twitter 和獨立開發者。


# 特點

在 Cassandra 的早期版本，其忠實呈現了 Google BigTable 或是 Hadoop (Wide-Column) 和 AWS DynamoDB (Key) 的資料模型。 無綱要 No-Schema 的資料模型代表著，其能動態地定義欄位 Column，但一體兩面的是缺點則暴露在很難決定資料的意義與格式，然而當資料變得很龐大的時候，則體現其擴展性的優點。

NoSQL 包含 sharding 擴展性的高度容錯、sort & search 查詢效能、de-centralize 分散式作業的三大特性，Cassandra 自然是具備的。


# 詳述 De-Centralization 

分散式架構主要特點當然是與主從式不同，它不具有集中管理者，每個 node 或每個 cluster 的功能和權限都是一樣的。

傳統的 SQL 這種關聯性資料庫，一旦遇到大量資料部署和擴張，大開大合的情境，會讓關聯性資料庫受窘迫，因為要維持交易的 ACID，則共享資源為了避免競奪，勢必會在某情況中符合某一條件下，將其資源上鎖，這會造成無法忍受的等待，和使用者極差的感受。

但是一但橫向擴展設備，每台機器或是虛擬機完成不同任務，又要協調和整合其任務結果，保持一制性又要保持效能性，需要在兩者之間取得雙贏和平衡。

# RollBack & Compensation

這樣就會讓系統架構師需要做到 2PC, 2 process commit 跨節點的協調以及分散式架構中的補償機制。（補充說明：補償機制即交易作業仍然維持已經遞交的狀態，但是交易成功與否，仍能以回滾方式取消。）


# Sharding, 分片 （擴展方式之一）

這類架構首先由 eBay 所採用，可以支撐到一天十億次的查詢情境。分片是將資料橫向拆分，座落在不同主機或是叢集中作業，各自獨立作業。

採取分片策略後，需要挑選一個好的主鍵，藉此排序資料。

分片策略具有的優勢特點是：最小化資源共用的風險以及可進行資源擴展。

# 主從到分散的緣由

關聯性資料庫固然在很多時候，也真的算上是時代性解決方案的最大贏家，但他僅僅解決某類型的資料存儲問題，由於集中性遇到大量資料需要擴展時，會需要備份和取消彼此的連結操作以避免被鎖死，這就是資料去中心化的原因囉！

# CQL, Cassandra Query Language 

也因為這一體兩面的特點，限制了其複雜查詢的表述（表達）能力。基於此緣故，Cassandra 導入自己的查詢語言。

此查詢語言介接 noSQL 和 RDBM 之間，有 Schema-Options 的選項。

# Install on Mac

  https://gist.github.com/hkhamm/a9a2b45dd749e5d3b3ae

(1) 設定 JAVA_HOME 環境變數：
    在環境變數名稱欄位新增 JAVA_HOME
    並在變數值欄位設定安裝 JAVA 或 JDK 或 JVM 的路徑

(2) 重新啟動終端機，藉以讓系統取得新增的變數，
    倘若環境變數和其值設定無誤，
    則可以在啟動 Cassandra 過程中找到 Java
    在終端機執行 echo %JAVA_HOME% 可以印出環境變數的值。

(3) 也可以順便設定 Cassandra 的環境變數和其值，
    有利之後倘若運用 cqlsh 或是 nodetool 等資料庫服務工具帶來便利的享受。
    
# Start Service

開啟終端機，並且移至目錄

    cd <cassandra-dir>/bin
    
>>>
然後，執行 cassandra -f 指令啟動服務

     cassandra -f
>>>     

啟動服務後，資料會建立在預設的 CASSANDRA_HOME 目錄中。

會有兩種資料，一是 data，一是 log。

另外，也能見到支援此資料庫的工具版本號，包含 Thrift API。

# default Port

    9160

# 關鍵字

初始化的資料結構

    key

    row

    counter

主機與叢集中其他節點的溝通介面

    JMX // Java Mgmt Plugin

    gossip

    clients
    
    state jump // 節點的啟動狀態
 
 這些日誌可供持續性的觀察，可紀錄週期性的輸出，包含 memcache 寫入磁碟等等。
 另外，如果安裝新版本 C*，最好刪除先前的日誌目錄，確保安全。

# Stop Service

    ./stop-server


