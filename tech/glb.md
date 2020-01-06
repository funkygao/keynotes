# 异地多活

## Overview

2018年9月份云栖大会上蚂蚁金服当场把杭州的2个IDC的网线剪短...

### Buzz Words

- 单元化 Set
   - 一个单元可以包含多个IDC，但通常对应一个IDC
- 就近访问
   - CDN
   - statefull vs stateless
- 异地多活
   - 数据同步是异地多活的基础
   - DB/Cache/MQ

### 容灾级别

- 单节点容灾
   - app/db/cache/mq broker
- rack容灾
- 机房容灾
   - 2个IDC并不具备机房容灾能力，至少需要3个IDC，因为zk/redis/etcd/consul等需要quorum
   - 部署3个节点，但只有2个IDC，那么节点分布必然(2, 1)，当2的IDC挂了，则剩下的节点/IDC无法形成quorum，无法正常工作
   - 3个IDC，每个IDC部署一个节点，那么一个IDC挂了还剩2节点，这就是“2地3中心”
- 城市容灾
   - 3地5中心(OceanBase)
      - 3个城市拥有IDC(2, 2, 1)
      - 1个城市发生灾难，其他2个城市至少保证3个IDC存活，可以形成quorum
- 国家故障
   - Spanner
