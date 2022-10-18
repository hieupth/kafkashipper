# kafkashipper
Microservice to make it easier to delivery packages in Kafka.

# Idea
- This will create a Kafka application that will deliver packages using Faust and 
communicate with Front-end with WebSocket.
</br>
```
     ws           kafka-stream
FE <----> Faust <--------------> Kafka-mcs
```
- FE will send data with bellow format to Faust server using Websocket: 

`JSON({'id': ... , 'header': ..., 'body': ...})` 

- Where _header_ is the ***list of mcs*** that project need,</br>
_data_ is the contain (text, image, etc.)</br>
_id_ is the identity of the FE.

- This Websocket is running in background will send the given message to 
Faust KafkaShipper topic and sent to the mcs(s). 

- Finally, this process will repeat until the list of header is empty and send back
to the FE through Websocket.

# Usages
- Run faust
```commandline
python faust_ws.py worker -l INFO --without-web
```
- Input format example:
```json
{
  "id": "1",
  "header": ["topic1", "topic2"],
  "body": ["hello world"]
}
```

And that's it. Try it on your own websocket.

