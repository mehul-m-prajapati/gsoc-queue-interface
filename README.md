## GSoC 2018: Queue interface
![Hex](https://img.shields.io/badge/gsoc-syslog--ng-blue.svg)

### General Info
- Name: Mehul Prajapati
- Github: [mehul-m-prajapati](https://github.com/mehul-m-prajapati)
- Email: mehulprajapati2802@gmail.com
- Organization: [syslog-ng](https://github.com/balabit/syslog-ng)
- Mentor: [Kókai Péter](https://github.com/Kokan)
- Development Branch: [queue-interface](https://github.com/mehul-m-prajapati/syslog-ng/tree/queue-interface)

### Project Abstract
> The syslog-ng has a queue for destinations, that has a current implementation as disk queue. The aim of this project is to develop a Redis based queue interface which could be an alternative to the disk queue.
> [Redis](https://github.com/antirez/redis) is an open source in-memory data structure store, used as a database, cache and message broker.

## Blog Posts:
- [Medium](https://medium.com/@Mehul2802/compiling-syslog-ng-source-code-on-ubuntu-16-04-9bd93ecf02ef)

## Design Diagram
```
 --------                    ----------------                    -------------
| Source | ================ | syslog-ng core | ================ | Destination | 
 --------                    ----------------                    -------------
                                   ||
                                   ||
                                   ||
                             ----------------      
                            |  redis queue   |
                            |    plugin      |
                             ----------------
```                          
## Commits


## Pull Request


## To Do (In Future)
- Implement reliable and non-reliable redis queue
- Limit number of messages that can be stored in redis (i.e. using overflow queue)
