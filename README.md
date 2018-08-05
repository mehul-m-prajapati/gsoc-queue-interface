![](https://camo.githubusercontent.com/ed508e9c66d718f76333215a139af24f8bb8fa8d/68747470733a2f2f6d75736573636f72652e6f72672f73697465732f6d75736573636f72652e6f72672f66696c65732f4361707475726525323064253237652543432538316372616e253230323031362d30332d303125323030392e34382e31315f302e706e67)

## GSoC 2018: Queue interface
![Hex](https://img.shields.io/badge/gsoc-syslog--ng-blue.svg)

### General Info
- Name: Mehul Prajapati
- Github: [mehul-m-prajapati](https://github.com/mehul-m-prajapati)
- Email: mehulprajapati2802@gmail.com
- Organization: [syslog-ng](https://github.com/balabit/syslog-ng)
- Mentor: [Kókai Péter](https://github.com/Kokan)

### Project Abstract
> The syslog-ng has a queue for destinations, that has a current implementation as disk queue. The aim of this project is to develop a Redis based queue interface which could be an alternative to the disk queue.
> [Redis](https://github.com/antirez/redis) is an open source in-memory data structure store, used as a database, cache and message broker.

## Blog Posts:
- [Medium](https://medium.com/@Mehul2802/compiling-syslog-ng-source-code-on-ubuntu-16-04-9bd93ecf02ef)

## Design Diagram


## Commits 


## Pull Request


## To Do (In Future)
- Implement reliable and non-reliable redis queue
- Limit number of messages that can be stored in redis (using overflow queue)
