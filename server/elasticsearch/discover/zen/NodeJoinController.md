handleJoinRequest
1. 若尚未成为主节点，还在票数积累阶段
    1. **积累票数**：调用ElectionContext的[addIncomingJoin](#addIncomingJoin)将请求添加到积累列表中
    2. **检查票数**：调用[checkPendingJoinAndElectIfNeeded](#checkPendingJoinAndElectIfNeeded)检查票数是否够了，如果不够不进行任何动作，如果够了则成为主节点，并开始处理请求
2. 已经成为主节点，则直接调用[MasterService](../../cluster/service/MasterService.md)的submitStateUpdateTasks来处理加入请求



<span id="checkPendingJoinsAndElectIfNeeded">**checkPendingJoinsAndElectIfNeeded**</span><br>
1.调用ElectionContext的[getPendingMasterJoinsCount](#getPendingMasterJoinsCount)方法获取当前票数
2. 如果没有够则不采取动作，如果票数够了，则调用ElectionContext的[closeAndBecomeMaster](#closeAndBecomeMaster)让当前节点成为主节点，并开始处理请求





## ElectionContext

<span id="addIncomingJoin">**addIncomingJoin**</span><br>
将收到的节点加入请求加入到请求累计列表中:key为要加入的节点对象，value为完成回调（MemebershipAciton完成加入返回请求使用）

<span id="getPendingMasterJoinsCount">**getPendingMasterJoinsCount**</span><br>
**获取票数**：遍历积累的加入集群请求，计数其中的主节点个数，并返回

<span id="">**closeAndBecomeMaster**</span><br>
1. 调用ElectionContext的[innerClose](#innerClose)来关闭ElectionContext
2. 将其他节点的加入请求任务，当前节点成为主节点的任务，结束选举的任务都加入任务列表
3. 调用[MasterService](../../cluster/service/MasterService.md)的submitStateUpdateTasks来执行这些任务

<span id="innerClose">**innerClose**</span><br>
使用原子类的getAndSet来将ElectionContext的原子布尔关闭标识``closed``设置为true, 表示ElectionConext已经关闭
