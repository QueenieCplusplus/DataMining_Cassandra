# DataMining_Cassandra
資料分析框架

# 起源

2007 年由臉書團隊為了解決收件箱太多資料要處理，但需要擴張的問題，而設計的讓資料得以複製與修改，且能隨時讀寫的後端資料庫系統架構，直至 201年方才成熟。

目前貢獻的遞交者包含蘋果、LinkedIn、Twitter 和獨立開發者。


# 特點

在 Cassandra 的早期版本，其忠實呈現了 Google BigTable 或是 Hadoop (Wide-Column) 和 AWS DynamoDB (Key) 的資料模型。 無綱要 No-Schema 的資料模型代表著，其能動態地定義欄位 Column，但一體兩面的是缺點則暴露在很難決定資料的意義與格式，然而當資料變得很龐大的時候，則體現其擴展性的優點。

NoSQL 的擴展性的高度容錯、查詢效能、分散式作業，Cassandra 自然是具備的。


# 詳述 De-Centralization 

分散式架構主要特點當然是與主從式不同，它不具有集中管理者，每個 node 或每個 cluster 的功能和權限都是一樣的。

傳統的 SQL 這種關聯性資料庫，一旦遇到大量資料部署和擴張，大開大合的情境，會讓關聯性資料庫受窘迫，因為要維持交易的 ACID，則共享資源為了避免競奪，勢必會在某情況中符合某一條件下，將其資源上鎖，這會造成無法忍受的等待，和使用者極差的感受。

# CQL, Cassandra Query Language 

也因為這一體兩面的特點，限制了其複雜查詢的表述（表達）能力。基於此緣故，Cassandra 導入自己的查詢語言。

此查詢語言介接 noSQL 和 RDBM 之間，有 Schema-Options 的選項。

