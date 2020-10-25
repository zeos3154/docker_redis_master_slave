redis 5.0.8 一主两从 +哨兵模式

redis.conf文件中需要设置daeonize no，设置前台运行，如果指定为yes，redis会以守护进程的方式在后台运行，根据docker要求至少有一个前台进程的特性，就会导致redis自动退出，加上docker-compose文件中设置为restart:always，对外展示就是一直处于restarting状态

哨兵模式需要进入到容器里面执行redis-sentinel sentinel.conf开启
