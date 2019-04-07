**定义一个Transport接口的处理handler**<br>
要实现一个Transport接口要实现一个[TransportRequest](./TransportRequest.md)的子类，和TransportRequestHandler的一个具体实现，然后调用[TransportService](./TransportService.md)的registerRequestHandler方法来完成注册。<br>
该handler主要定义了一个messageReceived方法，用于在接口被调用时回调。<br>
**TODO:** 了解带task参数的函数
```
package org.elasticsearch.transport;

import org.elasticsearch.tasks.Task;
public interface TransportRequestHandler<T extends TransportRequest> {

    /**
     * Override this method if access to the Task parameter is needed
     */
    default void messageReceived(final T request, final TransportChannel channel, Task task) throws Exception {
        messageReceived(request, channel);
    }

    void messageReceived(T request, TransportChannel channel) throws Exception;
}
```
