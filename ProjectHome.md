# Muduo - A C++ non-blocking multi-threaded network library for Linux #

Source code repository: https://github.com/chenshuo/muduo

Download tarballs: https://github.com/chenshuo/muduo/releases [latest](https://github.com/chenshuo/muduo/releases/latest)

Introduction slides: http://www.slideshare.net/chenshuo/muduo-network-library

## Goals ##
  * Small code base, less than 5,000 lines of code
  * A library, not a framework
  * Thread safe and efficient, minimize locking
    * Support multi-threading out-of-box
    * Single thread as a special case of multi-threads.
  * Simplifies network programming by supporting only one established event-driven model:
    * One event loop per thread, with non-blocking IO
    * Each connection/acceptor/timer is bound to one reactor
    * Events happen in predictable thread
  * Focus on server side
    * Support single-threaded and thread-pool configuration
    * Auto retry connecting with back-off intervals
    * Provide an embedded http server for querying the heath of process
    * Suitable for in house network programming on Linux
  * Linux on x86-64 as the main platform, also support IA32.
  * Scale up to 50k concurrent TCP connections, with epoll(4)

### Interface Design ###
  * Easy to use, once you get used to it :)
  * Callback-centralized interface, heavily utilize `boost::function<>`
  * Prefer object-based paradigm, rather than object-oriented or template-based
    * All exposed classes are concrete classes
    * Do not expose any virtual functions to user, opposite to ACE
    * Do not expose any class templates to user, opposite to Boost.Asio
  * `shared_ptr` for `TcpConnection` objects
  * Only uses classes available in STL and TR1 (shared\_ptr mainly)
  * **No exception thrown**

### Internal Design ###
  * Utilize recent kernel improvements: eventfd, signalfd and timerfd
  * Sub-millisecond precision for timer callbacks
  * RAII everywhere, no `delete` statements
  * Compiles cleanly with `-Wall -Wextra -Werror`
  * Separate internal classes and interface classes, use Pimpl to hide details.
  * See ClassDiagram

### Muduo doesn't ###
  * Aim for extreme high throughput, which harms clear design
  * Aim for extreme elegant design, which harms performance and usability
  * Support transport protocols other than TCPv4
  * Cross platform, you may use ACE/Asio/Java instead
  * Support Other IO model, eg. blocking IO, asynchronous IO or proactor
    * One event loop per thread is good enough for daily life network programming
  * Provide flexible and comprehensive solution for all networking area, one size never fits all

## Getting started ##
  * BuildMuduo
  * MuduoTutorial
  * MuduoThreadModel
  * MuduoExamples