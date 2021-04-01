该类为抽象类，且已过时，用于抽象所有需要日志的组件
```
/**
 * @deprecated declare your own logger
 */
@Deprecated
public abstract class AbstractComponent {

    protected final Logger logger;

    public AbstractComponent() {
        this.logger = LogManager.getLogger(getClass());
    }
}
```
