总共会有下面这几大模块
缓冲区
http的处理
webserver
线程池
对象池
连接池
日志

对于高并发模式：支持reactor和proactor
reactor只能采用epoll + 非阻塞 + 边沿触发
proactor采用AIO作为IO多路复用机制

对于数据库，考虑使用MYSQL作为主存储数据库，
使用redis来优化查询效率

环形缓冲区还有一大优势就是可以避免reset的次数

如何去关闭一个服务器程序呢,使用简单的CTRL + C吗,这样确实可以关闭程序.
但是试想这样一种场景,一些客户正在等待服务端的响应,但是却直接关闭了.
普通的任务当然没有关系,但是如果是非常重要的任务呢,比如交易.
因此我们需要对服务器的关闭也做一些优化,可以使用信号注册来关闭程序.我们自定义
一个接收的函数,使得服务端不会再接收新的连接,只会将当前的任务处理完成

对于最后的测试，使用GTEST和webrench来完成

使用reactor模拟proactor来进行完成
需要对缓冲区重新进行设计，设计两段区间以及是否需要两段区间的标志
