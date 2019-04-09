### 1.简要描述
**<font style="color:Orange">节点故障检测抽象类</font>**<br>
1. **<font style="color:Orange">注册连接断开监听器</font>**：该类通过在构造时调用[TransportService](../../transport/TransportService.md)的addConnnectionListener接口注册TransportPort连接变更监听器，并实现了[TransportConnectionListener](../../transport/TransportConnectionListener)的一个具体实现FDConnectionListener，
