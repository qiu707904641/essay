# 目录
1. [小猪券包](https://github.com/qiu707904641/essay?tab=readme-ov-file#%E5%B0%8F%E7%8C%AA%E5%88%B8%E5%8C%85)
## 小猪券包
- 制作背景
- 架构图
![小猪券包 drawio](https://github.com/qiu707904641/essay/assets/56197153/44f81430-98ec-44b7-bd1e-53fba46774e3)
## mongodb
- docker compose file
```
  version: '3.8'
  
  services:
    mongo1:
      image: mongo
      container_name: mongo1
      command: --replSet "rs0" --bind_ip 0.0.0.0
      ports:
        - 27011:27017
    mongo2:
      image: mongo
      container_name: mongo2
      command: --replSet "rs0" --bind_ip 0.0.0.0
      ports:
        - 27012:27017
    mongo3:
      image: mongo
      container_name: mongo3
      command: --replSet "rs0" --bind_ip 0.0.0.0
      ports:
        - 27013:27017
```
- 任意选择一个容器作为主节点,进入该容器`docker exec -it container_id /bin/sh`；进入mongosh命令行`mongosh`，执行副本集初始化命令`rs.initiate({_id:"rs0", members:[{ _id: 1, host: "192.168.10.40:27011" }, { _id: 2, host: "192.168.10.40:27012" }, { _id: 3, host: "192.168.10.40:27013" }]})`，其中192.168.10.40为本机内网地址，官方文档强烈建议使用dns服务器地址，避免因为mongod实例ip变更而导致不可用；检查集群配置`rs.conf()`
