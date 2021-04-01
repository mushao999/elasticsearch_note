## 1. 总结
抽象了一个生命周期管理组件的监听器，注册给索引生命周期组件可以在该组件发生各类状态变化时触发对应的动作

## 2. 源码
[org.elasticsearch.common.component.LifecycleListener](https://github.com/elastic/elasticsearch/blob/6.7/server/src/main/java/org/elasticsearch/common/component/LifecycleListener.java)
```
public abstract class LifecycleListener {

    public void beforeStart() {
    }

    public void afterStart() {
    }

    public void beforeStop() {
    }

    public void afterStop() {
    }

    public void beforeClose() {
    }

    public void afterClose() {
    }
}
```