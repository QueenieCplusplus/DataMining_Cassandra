# Cassandra

![C*](https://miro.medium.com/max/810/0*yluBx-0hOMU3djHf.png)

# ------------------------------------------------------------------------------------------

# C * Client, 客戶端的資料庫驅動程式

# ------------------------------------------------------------------------------------------

<h2> Concept of Know-How

We as client use the Client Driver to connect with the DB, we develop the
DB app and connect it with real DB with this client driver.

In my personal case, there is a Mongoose Driver for MongoDB using nodejs & SQLAlchemy Driver for MariaDB using python, and now it is time to use Cassandra DB Engine and its driver called 'datastax'.

In older version of C*, there remains the Hector && Astyanax and so on...(including Pycassa).

------------------------------------------------------------------------------------------

<h2> DataStax Driver 

support by Python || C/C++ || Java

<https://docs.datastax.com/en/landing_page/doc/landing_page/newDev.html>

------------------------------------------------------------------------------------------

<h2> Config in Env for Dev

To install & load the driver and its dependencies in EnvPath. In case of Java, we use the Maven as Pkg Manager. And add some lines to its pom.xml files.

        <dependency>
            <groupId> com.datastax.cassandra </groupId>
            <artifactId> cassandra-driver-core </artifactId>
            <version> </version>
        </dependency>

see ref doc, plz google github/datastax/java-driver || python-driver

------------------------------------------------------------------------------------------

* Connection to Cluster

        // create a cluster instance
        Cluster cluester = Cluster.builder().addContactPoint("127.0.0.5").build();

        // to initialize the cluster instance
        cluster.init();
        // it will call and trig the driver to make connection (any IP provided by client)
        // if the connection error or exception occurs, then it raises the NoHostAvailableException. 

The DB app using the driver API to connect with C*'s Cluster, it belongs to
com.datastax.driver.core.Cluster && class called Session.

The class called Cluster is the entry point, and it leads to the Fluent-Style API. (流式)

------------------------------------------------------------------------------------------

# ------------------------------------------------------------------------------------------

# Session, 會議連線模式(持久的連線)

# ------------------------------------------------------------------------------------------

<h3> Session Instance by calling connect()

* use Sessions to make real connection with Cluster doing db operation


----- 

        to create the session instance to do db pos
        we can re-use one Session Instance to do many ops in a Life Cycle,due to High-Cost
        it because of a session maintains all cluster nodes in the pool
        Once an app covers many keyspaces, the session then will be created by keyspace to keyspace.

        // create the cluster inastance then create a session instance
        Session ss = cluster.connect(keyspaceInStringFormate);

        // .connect() can be called instead of calling .init()

------------------------------------------------------------------------------------------

<h3> Sessions & Http_Limit_Requests

One connection build a session, and a session maintains all the only-one-connector for all the clusters nodes in the pool.

This only-one-connector allows many requests at the same time, the allows-many-requests means "http_limit_req",

see <https://segmentfault.com/a/1190000004688125>

seems like the graph below:

![session and nodes in pool](https://docs.jboss.org/jbossas/jboss4guide/r4/html/images/clustering-BalancerArch.png)

# ------------------------------------------------------------------------------------------

# CQL, Cassandra SQL statement, 資料庫敘述句

# ------------------------------------------------------------------------------------------

(to be continued...)


<h3> Mappig Manager


------------------------------------------------------------------------------------------

<h3> Query Builder


------------------------------------------------------------------------------------------

<h3> Ad Hoc Query using Simple Statement


------------------------------------------------------------------------------------------

<h3> Prepared Statement (Reusage & Avoid SQL Injection), 預備敘述


> UML

        App or WebBrowser send Http_Requests ------>  LB -----> Nodes in Pool using Cassandra Engine


> create Prepared Statement using Session.prepare()

        // create cluster instance and make session for nodes in pool (for a life cycle)

        Cluster cluester = Cluster.builder().addContactPoint("127.0.0.5").build();
        Session ss = cluster.connect('queens_cat'); // param passes the keyspace
        
        // create insstance of PS
        // pass param which is a SQL-statement
        // Insert Into Field Value

        PreparedStatement catFieldInsertPrepared = ss.prepare("INSERT INTO queens_cat(id, date) VALUE(?, ?) ");

        // create insstance of PS
        // pass param which is a SQL-statement
        // Select all From Table WHERE key is __

        PreparedStatement catFiledSeletPrepared = ss.prepare("SELECT * FROM　queens_cat Where id=?");

> PreparedID, 唯一識別符號

    Notice : the class of PreparedStatement is not the child class from parent class called 'Statement'. Because of it, the Type Error will not occurs and TypeExeception will not be raised due to the PS make Type of passing Param avoids from mentioned error & exception.


                // by calling its attrs to chek its ID of PS.
                catFieldSelectPrepared.getPreparedID()   

------------------------------------------------------------------------------------------

<h3> Bound Statement, 限制敘述句

> To Pass Value by calling bind()

                catFiledSeletPrepared.BIND(318) # PASS VAL // 綑綁敘述句

> binding Val

                BoundStatement catFieldSelectBound = catFieldSelectPrepared.bind("poupou2018") // pass val by pass param using bind()

> Set Its Attrs Val

                catFieldSelectBound.setString("name", "queens poupou")


------------------------------------------------------------------------------------------

<h3> Async Execution


# ------------------------------------------------------------------------------------------

# Security Issues, 安全機制

# ------------------------------------------------------------------------------------------

* Plugin of Encyption (Cypher) and Authentication

        create an instance using interface called com.datastax.driver.core.AuthProvider, and assign to Cluster.Builder.withAuthProvider()

       // create a auth instance
       AuthProvider auth_p 

       // assign it to the Cluster.Builder.withAuthProvider()
       Cluster.Builder.withAuthProvider(auth_p)

         or I guess: using the below instance of custer

        cluster.Build.withAuthProvider(auth_p)

       // create a cluster instance
        Cluster cluester = Cluster.builder().addContactPoint("127.0.0.5").build();

        // to initialize the cluster instance
        cluster.init();
        // it will call and trig the driver to make connection (any IP provided by client)
        // if the connection error or exception occurs, then it raises the NoHostAvailableException. 
        // if not able to pass the Auth, then it raises the AuthenticationException.

# ------------------------------------------------------------------------------------------

# Deploy (Network), 網路與資源佈署

# ------------------------------------------------------------------------------------------

(to be continued...)

------------------------------------------------------------------------------------------

* Monitor


------------------------------------------------------------------------------------------

* Host


------------------------------------------------------------------------------------------

* Adjust


------------------------------------------------------------------------------------------

* Access MetaData


------------------------------------------------------------------------------------------

* Adress Translator


------------------------------------------------------------------------------------------

* Retry Policy  


------------------------------------------------------------------------------------------

* Spec Execution


------------------------------------------------------------------------------------------

* LB Policy

------------------------------------------------------------------------------------------

# ------------------------------------------------------------------------------------------

# Architecture, 架構

# ------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------

# About NoSQL 

(to be continued...)

------------------------------------------------------------------------------------------

# Data Model

(to be continued...)

------------------------------------------------------------------------------------------
