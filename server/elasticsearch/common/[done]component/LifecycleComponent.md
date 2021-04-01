## 1. 总结
支持生命周期特性的组件的抽象，这类组件可以：
- 执行开始，停止操作
- 获取当前组件的生命周期状态
- 添加和删除生命周期listener

目前在ES中实现该接口的有(**在接口extends这个接口，在实现中extends AbstractLifecycleComponent**)
- AbstractLifecycleComponent： 一个通用的生命周期组件实现抽象类
- Discovery接口
- HttpServerTransport接口
- Repository接口
- Transport接口
## 2. 源码
[org.elasticsearch.common.component.LifecycleComponent](https://github.com/elastic/elasticsearch/blob/6.7/server/src/main/java/org/elasticsearch/common/component/LifecycleComponent.java)
```
public interface LifecycleComponent extends Releasable {

    Lifecycle.State lifecycleState();

    void addLifecycleListener(LifecycleListener listener);

    void removeLifecycleListener(LifecycleListener listener);

    void start();

    void stop();
}
```