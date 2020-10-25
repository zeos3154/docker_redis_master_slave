redis 5.0.8 一主两从 +哨兵模式

redis.conf文件中需要设置daemonize no，设置前台运行，如果指定为yes，redis会以守护进程的方式在后台运行，根据docker要求至少有一个前台进程的特性，就会导致redis自动退出，加上docker-compose文件中设置为restart:always，对外展示就是一直处于restarting状态

sentienl开启之后配置文件会不断变化，提供一份基础配置
sentinel.conf
  #哨兵需要后台启动
  daemonize yes
  #指定master节点的ip和端口（主）
  sentinel monitor mymaster localhost 6379 2  
  #指定master节点的ip和端口（从）
  sentinel monitor mymaster master 6379 2       
  #哨兵多久监听一次redis架构（此处为10s）
  sentinel down-after-milliseconds mymaster 10000 

哨兵模式需要进入到容器里面执行redis-sentinel sentinel.conf开启
