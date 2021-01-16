# System Design



## 考试形式

* 设计一个xxx系统
* 设计某个xxx系统的zzz功能





## 模板 Tree (4S)

1. Scenerio 

    * Feature:
    
            feature_0, feature_1, feature_2, feature_3 ... (按重要性排序)
                
    * Scope:
    
            Estimate:     
                DAU (Daily Active User) : 100M （读)
                每个用户每天访问次数 : k
                估算read QPS (average) : DAU * k / (24 * 60 * 60) = m/s
                估算read QPS峰值 (peek) : m * 10 = n/s
                估算write QPS ： n / 100 = j/s
            
            Common Params:
                Web Server: QPS (每秒能承受多少次用户并发访问) 
                    QPS = 100 -> 一台普通笔记本做web server即可
                    QPS = 1k  -> 一台好点企业级web server (30-40 core) 优化了缓存功能，考虑了逻辑处理和数据库查询瓶颈；考虑Single Point Failure问题
                    QPS = 1m  -> 需要搭设一个1000台web服务器集群；考虑如何 Maintain
                
                DB: QPS (每秒能承受多少次数据读取请求) 
                    一台SQL db的承受量是1k的QPS (如果Join和Index 比较多，这个值会更小)
                    一台NoSQL db (Cassandra) 的承受量是10k的PQS
                    一台NoSQL db (Memcached) 的承受o量是1M的QPS
                
2. Service

    * 再过一遍功能需求，为每个需求添加一个服务
    * 归并相同的服务
    * Service就是整个系统被肢解后的独立服务模块
        
    
3. Storage

    > 程序 = 数据结构 + 算法
    > 系统 = 服务 + 数据存储
    

    * 为每个service 选择合适的数据存储引擎
    
    [select storage engine for each service](imagePool/serviceStorage.png)
    
            Database
                * Sql DB
                * Nosql DB
            File System
            Cache 
            
    * 细化数据表结构 (SQL Schema)
    

    
    

