## GSoC 2018: Queue interface
![Hex](https://img.shields.io/badge/gsoc-syslog--ng-blue.svg)

### General Info
- Name: Mehul Prajapati
- Github: [mehul-m-prajapati](https://github.com/mehul-m-prajapati)
- Email: mehulprajapati2802@gmail.com
- Organization: [syslog-ng](https://github.com/balabit/syslog-ng)
- Mentor: [Kókai Péter](https://github.com/Kokan)
- Development Branch Tag: [gsoc-2018](https://github.com/mehul-m-prajapati/syslog-ng/tree/gsoc-2018)

### Project Abstract
> The syslog-ng has a queue for destinations, that has a current implementation as disk queue. The aim of this project is to develop a Redis based queue interface which could be an alternative to the disk queue.
> [Redis](https://github.com/antirez/redis) is an open source in-memory data structure store, used as a database, cache and message broker.

### Blog Posts:
- [Medium](https://medium.com/@Mehul2802/compiling-syslog-ng-source-code-on-ubuntu-16-04-9bd93ecf02ef)

### Design Diagram
```
 --------                    ----------------                    -------------
| Source | ================ | syslog-ng core | ================ | Destination | 
 --------                    ----------------          ||        -------------
                                                       ||
                                                       ||
                                                       ||
                                                 ---------------      
                                                |  redis queue  |
                                                |    plugin     |
                                                 ---------------
```                          
---

### Commits / Tasks
- [X] [Develop dummy redis queue plugin](https://github.com/mehul-m-prajapati/syslog-ng/commit/f450a498dbf71d8f274047b5ee88830a664e0425)
- [X] [Add push, pop, ack, rewind backlog log queue methods](https://github.com/mehul-m-prajapati/syslog-ng/commit/f450a498dbf71d8f274047b5ee88830a664e0425)
- [X] [Add redis server connection methods instead of dummy queue](https://github.com/mehul-m-prajapati/syslog-ng/commit/aa4d15e52a74d562a5ae32bd10b6904759809111)
- [X] [Develop redis read, write and delete methods](https://github.com/mehul-m-prajapati/syslog-ng/commit/d27ef47669bcfa45e47c3b838921c0721fabbcbb)
- [X] [Add following configurable parameters for redis queue plugin](https://github.com/mehul-m-prajapati/syslog-ng/commit/0ef82502f218a16ce891301611d653b9b9ca9820)
* host address
* port
* auth
* key name prefix
* conn-timeout
- [X] [Handle backlog messages](https://github.com/mehul-m-prajapati/syslog-ng/commit/eac566f3417987b33dc9fd20423ab978890719cb)
- [X] [Develop unit test cases](https://github.com/mehul-m-prajapati/syslog-ng/commit/24121a18798004e6696b65ad7624ddb86284997d)
- [X] [Implement rqtool to print-out data from redis server (Useful for debugging)](https://github.com/mehul-m-prajapati/syslog-ng/commit/62666321c48464057ca9dbac4f3008d9d6900a98)
- [X] [Develop Redis connect, disconnect, reconnect, isconnected and send command methods](https://github.com/mehul-m-prajapati/syslog-ng/commit/1859d07733060703c87e6a38f299ceae8462ca3a)
- [X] [Add Redis SET for listing only redis queues in rqtool](https://github.com/mehul-m-prajapati/syslog-ng/commit/d8d569ab4bf2f6bd3cef3e654b40231282e9da1f)

### Pull Request (This link might get changed in future because of code review modifications)
- [balabit/syslog-ng/#2231](https://github.com/balabit/syslog-ng/pull/2231)

---
### To Do (In Future)
- Develop functional test cases in python
- Implement reliable and non-reliable redis queue
- Limit number of messages that can be stored in redis (i.e. using overflow queue)
- Redis as a cluster
- Merge rqtool and dqtool functionalities and develop qtool
