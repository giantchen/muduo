# Class diagram of Muduo #

![http://muduo.googlecode.com/files/muduo_class_diagram.png](http://muduo.googlecode.com/files/muduo_class_diagram.png)

## User visible classes in white background ##
  * EventLoop is a reactor, or event dispatcher.
  * TcpConnection is an _established_ TCP connection. TcpConnection is managed by shared\_ptr<>.
  * TcpConnection has two Buffer(s), one for input, the other for output.
  * TcpClient creates TcpConnection when connecting finishes.
  * TcpServer creates one TcpConnection per accept(2)-ion.

## Internal classes in gray background ##
  * Acceptor, owned and used by TcpServer.
  * Connector, owned and used by TcpClient.
  * Socket, owned and used by TcpConnection, it owns the socket file descriptor. When it destructs, fd will be close(2)d.
  * Poller, base class, owned and used by EventLoop
    * PollPoller, derived from Poller, uses poll(2)
    * EPollPoller, derived from Poller, uses epoll(4)
  * Channel, event handler, de-mux events to different callbacks.