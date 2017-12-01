# EnableEdgeIntelligence
Enable edge intelligence with Azure IoT Edge (my notes from the Connect(); session)

### Video
Enable edge intelligence with Azure IoT Edge by Arjmand Samuel 
https://channel9.msdn.com/events/Connect/2017/B114

## IoT in the Cloud and on the Edge
![IoT in the Cloud and on the Edge](/images/1_IoT_in_the_Cloud_and_on_the_Edge.png)

The cloud provides the ability to monitor your devices, which may be remote, which may be spread around the world. So the cloud gives you a way to bring them all together in one place and manage them. And it also allows you to have a monitoring from these devices and do things like ML in the cloud for which you need near infinite resources in storage  in the cloud.
Very insightful processes run on top of your data => AI, ML….


Edge --> your operations happening in your own facilities, this operations requires very tight low latency  control loops, which you need to execute right there next to your machines.  Azure IoT Edge allows you to do that. You maybe also need a protocol translation, imagine you have an modbus (https://es.wikipedia.org/wiki/Modbus) protocol internally and you want to provide translate into other kind of Internet protocols (maybe you have privacy reasons, and you don't want to send it).

IoT Edge allows you to have all the power you have in the cloud and take it all in the Edge.

Symmetry => you have the same programming models that you have in the cloud which you can bring to the edge. 
Your developers don't need other skills to program the devices.

