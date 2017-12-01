# Enable Edge Intelligence with Azure IoT Edge

 (my notes from the Connect(); session)

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

![Operational patterns for Azure IoT Edge](/images/2_Operational_patterns_for_Azure_IoTEdge.png)


**Protocol Translation**: pretty common to have a Modbus or other protocol, and want to translate them into IoT protocols like MQTT.

**On-prem data aggregation**: Do analysis in the device: save bandwidth = save cost = privacy Intellectual Property (IP). Analyze data and aggregate data on premise. 

**Offline**: Another interesting operational pattern that we've seen is offline. Perhaps its short-term offline  or long-term offline. So you might have a device or a few of them, deployed in a ship, and that seals off and then  you don't have connection, but you want  to still continue doing the same kind of intelligence in kind of Analytics , which you were doing previously with the cloud. 

**Intelligence at the edge**: The scenario where IoT Edge really shines is…. Allowing you to bring the cloud services that we have in the cloud and have that power, that intelligence deployed onto the devices onto your edge devices (like AI or ML from the cloud and deploy it onto a edge device). => Training your models in the cloud (requires a lot of resources) and then you can bring it down to the edge.
Stream analytics is another service that we have which you can already run jobs in the cloud and you actually have the same job: you can deploy it onto the edge (including developed in several languages)

