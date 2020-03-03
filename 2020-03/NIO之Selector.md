# NIO之Selector(选择器)

## 介绍
Selector 一般称 为选择器 ，当然你也可以翻译为 多路复用器 。它是Java NIO核心组件中的一个，用于检查一个或多个NIO Channel（通道）的状态是否处于可读、可写。如此可以实现单线程管理多个channels,也就是可以管理多个网络链接。
使用Selector的好处在于： 使用更少的线程来就可以来处理通道了， 相比使用多个线程，避免了线程上下文切换带来的开销。

## 注意事项
注册channel通道到selector组件上，需要把这个channel设置为非阻塞模式(官方提供的selector用法可以看出，需要用户自己手动循环检查selector的状态，并获取可用的IO,如果channel为阻塞模式的话，会把轮询检查selector状态给阻塞住)
```
官方demo
ByteBuffer buffer = ByteBuffer.allocate(1024); //缓冲区大小
Selector selector = Selector.open();
ServerSocketChannel channel = ServerSocketChannel.open(); //创建socket信道
channel.configureBlocking(false);//设置为非阻塞方式
channel.socket().bind(new InetSocketAddress(8080));
channel.register(selector, SelectionKey.OP_ACCEPT);//注册监听事件
while (true) {
  Set selectedKeys = selector.selectedKeys();//取得所有发生事件的key集合
  Iterator it = selectedKeys.iterator();
  //检查keys中所有事件的类型
  while (it.hasNext()) {
    SelectionKey key = (SelectionKey) it.next();
    //未监听到就绪事件
    if ((key.readyOps() & SelectionKey.OP_ACCEPT) == SelectionKey.OP_ACCEPT) {
      ServerSocketChannel ssChannel = (ServerSocketChannel) key.channel();
      SocketChannel sc = ssChannel.accept();//接受到服务端的请求
      sc.configureBlocking(false); //设置为非阻塞
      sc.register(selector, SelectionKey.OP_READ);
      it.remove();
    }
    //监听到就绪事件
    else if ((key.readyOps() & SelectionKey.OP_READ) == SelectionKey.OP_READ) {
      SocketChannel sc = (SocketChannel) key.channel();
      while (true) {
        buffer.clear();
        int n = sc.read(buffer);//读取数据
        if (n <= 0) {
          break;
        }
        buffer.flip();
      }
      it.remove();
    }
  }
}
```

## selector的常用状态
+ SelectionKey.OP_ACCEPT —— 接收连接继续事件，表示服务器监听到了客户连接，服务器可以接收这个连接了
+ SelectionKey.OP_CONNECT —— 连接就绪事件，表示客户与服务器的连接已经建立成功
+ SelectionKey.OP_READ —— 读就绪事件，表示通道中已经有了可读的数据，可以执行读操作了（通道目前有数据，可以进行读操作了）
+ SelectionKey.OP_WRITE —— 写就绪事件，表示已经可以向通道写数据了（通道目前可以用于写操作）
