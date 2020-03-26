# Filebeat

总体设计

log -> Harvestor -> Spooler -> Logstash/Kafka...

Harvestor: 读取文件信息

Spooler: 文件读取，Harvestor的信息写入和Output消费

Harvestor的启动：Filebeat刚启动的时候，会有一个注册Registrar记录文件状态，主要文件状态就是：offset, finishe. 我们需要Registrar来判断log是否已读或者是否读完成：

1. 如果Harvestor找不到该文件记录，那么新启动一个Harvestor，修改offset

2. 如果已经有Harvestor读取，那么finished为false

3. 如果已经读取结束，那么finished为true

Product: input -> (event) -> queue -> consumer

Consumer: 缓存 -> eventloop -> ClientWorker

ACK机制

