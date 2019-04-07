该类为抽象类，用于抽象出组件均需要的日志，过期日志，配置等信息，并提供了获取节点名字的方法
```
package org.elasticsearch.common.component;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.elasticsearch.common.logging.DeprecationLogger;
import org.elasticsearch.common.settings.Settings;
import org.elasticsearch.node.Node;
public abstract class AbstractComponent {

    protected final Logger logger;
    protected final DeprecationLogger deprecationLogger;
    protected final Settings settings;

    public AbstractComponent(Settings settings) {
        this.logger = LogManager.getLogger(getClass());
        this.deprecationLogger = new DeprecationLogger(logger);
        this.settings = settings;
    }

    /**
     * Returns the nodes name from the settings or the empty string if not set.
     */
    public final String nodeName() {
        return Node.NODE_NAME_SETTING.get(settings);
    }
}
```
