
初始化时，生成MemberAction对象，传入了一个MembershipListener
```
  private class MembershipListener implements MembershipAction.MembershipListener {
      @Override
      public void onJoin(DiscoveryNode node, MembershipAction.JoinCallback callback) {
          handleJoinRequest(node, ZenDiscovery.this.clusterState(), callback);
      }

      @Override
      public void onLeave(DiscoveryNode node) {
          handleLeaveRequest(node);
      }
  }
```

处理加入请求使用的是handleJoinRequest函数：
1. 校验要加入的节点是否通过加入验证器的检查
2. 连接节点，并使用MembershipAction对象，向节点发送加入集群验证请求
3. 调用[NodeJoinController](./NodeJoinController.md)的handleJoinRequest方法来处理请求
