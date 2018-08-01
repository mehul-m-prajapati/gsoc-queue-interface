## Disk Buffer
- The disk-buffer mechanism for a general destination driver is the following: all messages that arrive to the client's destination driver are first written to disk, even before the destination driver tries to send the messages.

- The messages are then peeked from the destination queue before sending, but popped only if the underlying protocol of the destination driver reports back with success. 

- So in practice, the buffering happens all the time for all messages, not only when there are problems with the connection.

## Syslog-ng module and plugin
- syslog-ng is divided into a core and modules, the syslog-ng core itself does not have (small lie here) sources, destinations, it just a shell to connect those things.
- The sources, and destinations are plugable, and a plugin can be a source or a destination, and a few other things. But the module is that syslog-ng could load dynamically. And a module could contain one or more plugins. An example of this is the afsocket, that contains all network source and destination plugins. The module itself is the .so file that compiled.

## Redis module
- The redis has its own module, because it is only supports destination for now. In case of redis, (and many other cases) the destination just uses some 3rd party C library to communicate with the other side. Currently, we are using hiredis for this.
- As is redis has nothing special as a destination, it is a threaded destination, which means that it does not run in the main thread.
It has to communicate over the network, and that is usually blocking, the main thread does not have time for that.
- I think what is interesting here, that right now syslog-ng only sends date to redis but we do not fetch (probably that could work also via hiredis) but this is something that should be checked.

## Plugin and driver are same?
- Not quite, a plugin can be a driver. But with queue it gets tricky because there is also a plugin that different.
- So, destination drivers can have plugins, the only example of this is the disk queue. But, that plugin is not equal as the plugin related to the module. Every destination could have diskq.

## logqueue 
- It can be connected to the destination drivers. Each driver has a queue.
- If diskq is not configured it is just an in memory queue. The porpose of course mostly buffering. Actually, both the diskq and fifo has multiple queues (e.g. overflow, backlog, ...)

## In which format log messages are stored ?
- serialize/deserialize could convert a LogMessage and byte string

## How Redis queue should work ?
- When pushing message to the queue it just increment a counter, and when poping it can decrement and generate a dummy message.
It can store the messages in memory and forward them.

## What ref/unref does in syslog-ng ?
- It is related to memory management. This is just a memory reference counting, like in early Java.
- You should use ref when you obtain the object (that has ref/unref) and you tend to keep it after your functions and like pushing into a queue or saving into self related fields.

## Flow control testing
```
log {
  source (s_source);
  destination(d_destination);

  flags(flow-control);
};
```
- The trick that with file destination kinda hard to test flow control because for that you should have an unresponsive file system.
- I would recommend you to you network destination because in case of network destination, you configure for example 
``network("127.0.0.1" port(1111) redis-queue() );`` and you simple do not listen on that socket with any application. So, syslog-ng cannot send data there and in that case flow-control is activated.

- It is going to stop receiving log messages in the source or in case of redisq it should start to store items into redisq until it is possible. The diskq was limited by a file size. 
- And when you open the network port, it should just start to send data there from the queue. You can listen to it with netcat for example.

## rewind_backlog
- It is called when a destination tries to send out the massage, but it cannot, like not connection also when flow-control is triggered
the messages should be stopped, for flow control is the rewind all.
- The simple rewind is when message cannot be sent regardless of flow control.
- The rewind all is triggered by flow-control.

## logpath options (ack message)
- You have to push msg, logpath; and pop msg (deserialize), logpath (use via macro) in order to work, you did not need to push the logpath, instead of pushing the logpath, you have to ack the message there, push the message.
- And when you pop the message, you still have to call log_msg_ack, but with a logpath that says ack_needed = FALSE;

## brief idea on main loop worker?
- It is just a frame to handle jobs in threads, like a reader thread or a destination could scale
- syslogng could work also in single thread, there is an option ``threaded(no)``

## pop, push, ack and rewind
- let's call backlog as B, and the redis queue with R. The R is a queue, where messages are that have not been processed (waiting to be processed)
- The B is a queue, where there are messages that were in the R, but the destination started to process and we do not know yet if they have been successfully processed or not ...
- when a push_tail happens, the queue receives the message and it should put it into the R 
- when the pop_head is called, a destination is trying to process the message the message should be removed from R, and it should be putted into the B
- Ack will remove messages from B
- Rewind will get messages from B and put it to R
