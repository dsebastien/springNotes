# Spring Cloud Stream

* useful for message-driven micro-services
* builds upon Spring Boot
* opinionated configuration of message brokers
* supports multiple vendors
  * kafka
  * rabbitmq
  * activemq
  * redis
  * AWS Kinesis
  * ...

```
@EnableBinding(Sink.class)
```

...

```
@StreamListener(Sink.INPUT)
```

...

The following is enough to later be able to inject an output channel \(no implementation needed!\):

```
public class MyChannel {
    @Output("channelName")
    public MessageChannel outputChannel; 
}
```

Use like this to send a message to the channel:

```
@EnableBinding(MyChannel.class)
...
myChannel.outputChannel.send(MessageBuilder.withPayload(message).build());
```



