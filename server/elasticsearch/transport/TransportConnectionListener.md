**<font style="color:Orange">Transort连接变更监听器接口</font>**<br>
可以使用[TransportService](./TransportService)的addConnectionListener的注册，并实现对Transport连接的变更监听
``` go
package org.elasticsearch.transport;

import org.elasticsearch.cluster.node.DiscoveryNode;

/**
 * A listener interface that allows to react on transport events. All methods may be
 * executed on network threads. Consumers must fork in the case of long running or blocking
 * operations.
 */
//Michel: transport事件监听器的抽象接口定义，当发生对应时间时会调用定义的各方法，可以部分实现
public interface TransportConnectionListener {

    /**
     * Called once a connection was opened
     * @param connection the connection
     */
    default void onConnectionOpened(Transport.Connection connection) {}

    /**
     * Called once a connection ws closed.
     * @param connection the closed connection
     */
    default void onConnectionClosed(Transport.Connection connection) {}

    /**
     * Called once a node connection is opened and registered.
     */
    default void onNodeConnected(DiscoveryNode node) {}

    /**
     * Called once a node connection is closed and unregistered.
     */
    default void onNodeDisconnected(DiscoveryNode node) {}
}
```
