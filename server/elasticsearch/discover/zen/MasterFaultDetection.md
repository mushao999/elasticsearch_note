参考文章：
- [官方文档集群故障检测（ES7.x）](https://www.elastic.co/guide/en/elasticsearch/reference/7.x/cluster-fault-detection.html)
- [官方文档节点故障检测文档（ES6.7）](https://www.elastic.co/guide/en/elasticsearch/reference/6.7/modules-discovery-zen.html#fault-detection)
- [ElasticSearch Master、Node故障检测](https://www.jianshu.com/p/9f7282288858)

### 1.简述
**<font style="color:Orange">主节点故障检测类</font>**<br>
该类的功能主要有：
1. **<font style="color:Orange">主节点故障被动检测及处理（Listener）</font>**<br>：当前节点为非主节点时，注册一个主节点断开连接Listener，当主节点故障离开时则进行相应处理
2. **<font style="color:Orange">主节点故障主动检测及处理（Pinger）</font>**<br>：当前节点为非主节点时启动定时执行的ping任务，对主节点进行连接检测，如果出现异常进行相应的处理
3. **<font style="color:Orange">注册并实现响应主节点故障检测的接口（internal:discovery/zen/fd/master_ping）</font>**<br>：当前节点为主节点时，启动一个响应故障检测ping的接口，以响应非主节点的ping请求

### 2.详细解释
1. **主节点故障被动检查**：当前类继承自[FaultDetection](./FaultDetection.md)，重载该类的handleTransportDisconnect方法，来实现当有transport连接断开事件发生时，判断是否为主节点断开，如果是主节点断开则通知相应的Lisener。
