# 第x章：踩坑



### Kafka

1. Producer需要控制线程数量,不能直接创建线程,容易耗尽资源.

### Appolo

1. Map类型的配置,删除配置中Key不会同步删除服务器中的Key.详见[ Github](https://github.com/apolloconfig/apollo/issues/2719)描述.