# The thread model of Muduo #

One loop per thread.

## Classes ##

### EventLoop ###

  * Each thread may have at most one EventLoop object running.
  * It's a fatal error to create two EventLoop objects in the same thread, even without running it.


### TcpConnection ###

  * Each TcpConnection is associated with an EventLoop when created.
  * All IO happens in same thread of the EventLoop.
  * All event callbacks (onMessage and onConnection) happen in the thread which runs the event loop.

### TcpClient ###

  * TcpClient is associated with an EventLoop when created.
  * That EventLoop will be passed to TcpConnection when a new TCP connection is established.
  * So all IO happens in same thread of the EventLoop

### TcpServer ###
> There are two thread models of TcpServer:
  1. Single thread - all TcpConnection(s) share the same EventLoop.
  1. Thread pool - new TcpConnection(s) are assign to different EventLoop thread on a round-robin basis.


## Rationale ##

Due to the nature of non-blocking IO: