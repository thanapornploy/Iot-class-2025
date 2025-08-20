# Exploring MQTT QoS Levels

Experiment with QoS 0, 1, and 2.
Observe how message delivery changes based on QoS settings.

## Publisher_qos.py output

```
  client = mqtt.Client()
[15:23:54] DEBUG | Sending CONNECT (u0, p0, wr0, wq0, wf0, c1, k60) client_id=b''
Enter message to publish: [15:23:54] DEBUG | Received CONNACK (0, 0)
Fish
Enter QoS level (0, 1, 2): 2
[15:24:48] DEBUG | Sending PUBLISH (d0, q2, r0, m1), 'b'test/qos/6510301018/tempes
[15:24:48] PUBLISH REQUESTED | QoS=2 | Message='Fish' | msgid=1
Enter message to publish: [15:24:48] DEBUG | Received PUBREC (Mid: 1)
[15:24:48] DEBUG | Sending PUBREL (Mid: 1)
[15:24:48] DEBUG | Received PUBCOMP (Mid: 1)
[15:24:48] PUBLISHED | msgid=1
[15:24:55] DEBUG | Sending PINGREQ
[15:24:55] DEBUG | Received PINGRESP
[15:25:55] DEBUG | Sending PINGREQ
[15:25:55] DEBUG | Received PINGRESP
[15:26:56] DEBUG | Sending PINGREQ
[15:26:56] DEBUG | Received PINGRESP
[15:27:56] DEBUG | Sending PINGREQ
[15:27:56] DEBUG | Received PINGRESP
[15:28:57] DEBUG | Sending PINGREQ
[15:28:57] DEBUG | Received PINGRESP
[15:29:57] DEBUG | Sending PINGREQ
[15:29:57] DEBUG | Received PINGRESP
[15:30:58] DEBUG | Sending PINGREQ
[15:30:58] DEBUG | Received PINGRESP
[15:31:58] DEBUG | Sending PINGREQ
[15:31:58] DEBUG | Received PINGRESP
[15:32:59] DEBUG | Sending PINGREQ
[15:32:59] DEBUG | Received PINGRESP
[15:33:59] DEBUG | Sending PINGREQ
[15:33:59] DEBUG | Received PINGRESP

```

## Subscriber_qos.py Output

```
  client = mqtt.Client()
  client = mqtt.Client()
[15:23:40] DEBUG | Sending CONNECT (u0, p0, wr0, wq0, wf0, c1, k60) client_id=b''  client = mqtt.Client()
[15:23:40] DEBUG | Sending CONNECT (u0, p0, wr0, wq0, wf0, c1, k60) client_id=b''  client = mqtt.Client()
[15:23:40] DEBUG | Sending CONNECT (u0, p0, wr0, wq0, wf0, c1, k60) client_id=b''
[15:23:40] DEBUG | Received CONNACK (0, 0)
[15:23:40] Connected with result code 0
[15:23:40] DEBUG | Sending SUBSCRIBE (d0, m1) [(b'test/qos/6510301018', 2)]      
[15:23:40] DEBUG | Received SUBACK
[15:24:41] DEBUG | Sending PINGREQ
[15:24:41] DEBUG | Received PINGRESP
[15:25:41] DEBUG | Sending PINGREQ
[15:25:41] DEBUG | Received PINGRESP
[15:26:42] DEBUG | Sending PINGREQ
[15:26:42] DEBUG | Received PINGRESP
[15:27:42] DEBUG | Sending PINGREQ
[15:27:42] DEBUG | Received PINGRESP
[15:28:42] DEBUG | Sending PINGREQ
[15:28:42] DEBUG | Received PINGRESP
[15:29:43] DEBUG | Sending PINGREQ
[15:29:43] DEBUG | Received PINGRESP
[15:30:43] DEBUG | Sending PINGREQ
[15:30:43] DEBUG | Received PINGRESP
[15:31:44] DEBUG | Sending PINGREQ
[15:31:44] DEBUG | Received PINGRESP
[15:32:44] DEBUG | Sending PINGREQ
[15:32:44] DEBUG | Received PINGRESP
[15:33:45] DEBUG | Sending PINGREQ
[15:33:45] DEBUG | Received PINGRESP

```