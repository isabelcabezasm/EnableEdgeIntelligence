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

## Operational patterns for Azure IoT Edge
![Operational patterns for Azure IoT Edge](/images/2_Operational_patterns_for_Azure_IoTEdge.png)


**Protocol Translation**: pretty common to have a Modbus or other protocol, and want to translate them into IoT protocols like MQTT.

**On-prem data aggregation**: Do analysis in the device: save bandwidth = save cost = privacy Intellectual Property (IP). Analyze data and aggregate data on premise. 

**Offline**: Another interesting operational pattern that we've seen is offline. Perhaps its short-term offline  or long-term offline. So you might have a device or a few of them, deployed in a ship, and that seals off and then  you don't have connection, but you want  to still continue doing the same kind of intelligence in kind of Analytics , which you were doing previously with the cloud. 

**Intelligence at the edge**: The scenario where IoT Edge really shines is…. Allowing you to bring the cloud services that we have in the cloud and have that power, that intelligence deployed onto the devices onto your edge devices (like AI or ML from the cloud and deploy it onto a edge device). => Training your models in the cloud (requires a lot of resources) and then you can bring it down to the edge.
Stream analytics is another service that we have which you can already run jobs in the cloud and you actually have the same job: you can deploy it onto the edge (including developed in several languages)

## Pump Example
![Pump](/images/3_pump.png)

**Example** 

Pump to extract oil: All in remote, not a lot of operators are located next to the pump. 

Pressure above the plunger and pressure down the plunger (on the axis) 

### Today's SCADA solution
![Today's SCADA solution](/images/4_todays_scada_solution.png)

Well site (depósito/hueco) 

Next to the well there is a Gateway device, connected over Modbus. It goes up to SCADA controller (monitoring data) 
When the pump data goes out of any of those operational limits, you have to send the data (over mail, SMS, or… whatever) and send an alert to the operator who is off-site. 
The operator would look at the data and send somebody down to there (to adjust the pump)

Move data from well site to supervision site is expensive.
And once you do that you can actually also upload them to the cloud.

That's how is done today.

If you could take this power of the cloud and bring it down to the edge, right next to this pump.


### Example: Machine Learning on the Edge
![Example - ML on the Edge](/images/5_example.png)

Same pump, same gateway. 
Same Modbus.

IoT Hub in the cloud to upload all the data you have.

Modbus module next to the device. This Modbus module is doing the protocol translation.

It is picking up data and bring it up to the cloud, where you can train you ML models, but also you can  deploy those models down back on this IoT device and analysis (anomaly detection) and stop the pump, making the decision in the edge, without having to go up to the cloud and wait the latency.

Train in the cloud and run on the edge.

## Design principles:
### Secure
Provides a secure connection to the Azure IoT Edge, update software/firmware/config remotely, collect state and telemetry and monitor security of the device.
-> Go and work at the hardware layer from Azure (?)

### Cloud managed
Enables  rich management of Azure IoT Edge from Azure provide a complete solution instead of just an SDK.
-> You don't have to compile any code and put it on the device itself. You hosted somewhere and you can manage that device from the cloud. 

### Cross platform
Enables A IoT Edge to target the most popular edge OS, such Window and Linux.
-> We are building an IoT Edge, and we've built it to be cross platform. We support many versions of Linux and Windows on x64, on ARM… whatever gateway device or edge devices you have deployed on your prem. 

### Portable
Enables Dev/Test of edge workloads in the cloud with later deployment to the edge as part of a continuous integration /continuous deployment pipeline. 
-> Extremely portable. Any workload that you define in the cloud, you can simply bring them down to the edge. 

### Extensible:
Enables seamless deployment of advanced capabilities such as AI from MS and any third party, today and tomorrow.
-> Not only edge services like ML and AI. Also your own code. Innovate extensible fashion, 


So that's really some of the design principles  that we have for a Azure IoT Edge.

## Concept: Module
![Concept: Module](/images/6_concept_module.png)
**Module**: is a unit of compute

It could be parts of services which could be packaged as modules . All this modules are passed in containers and all of these containers are hosted in a repository somewhere.

We support Docker containers.


That is a module instance: when a module comes down and is deployed… let's say two devices: one in Germany, one in China. Those are module instances that are running over there. 


All of these module instances are brought down, monitored and controlled in the security provided by a component.
We call it the IoT Edge runtime.

![Concept: Module](/images/7_module.png)

**Each module has an identity**: important for security and authentication reasons. You should be able to address these modules from the cloud.

Each device has one ID. And each module have an address which indicate what modules are deployed into the device. 

You could have multiple modules instances deployed on any one device and there's way for us to go in and control an address them though an identity in the cloud

Each module also have a "Twin" in the cloud for the device.
You will have module twins and these modules (here you have the runtime status of every module) 

**Module twins** => JSON with the configuration (desired configuration, reported configuration… etc…)

The document pages are similar to the "device twins". <br /> 
It can be used to get the state of the module, send out data to the module from the cloud, and that gives you the control over the module and monitoring of what is happening on the monitor.

## Concept: Azure IoT Edge Runtime
![Concept: IoT Edge runtime](/images/8_concept_runtime.png)

**IoT Edge Runtime** sits on top of the device. <br/>
The device is connected to an IoT Hub and modules are sitting on top of it.
The runtime is the responsible for installing and updating all workloads on the device (heart of the system). It maintains the security so the runtime has access to all security tokens, the certification, the keys… which are in the hardware and it brings them up to each module for authentication….

It also ensures that there are always running so the modules are always running, so when you have a module going up, if there is an issue, runtime knows it and it would try to restart and all that information would be available in the IoT Hub, as the status of the devices and modules.

The runtime reports health and all the communication happening between leaf devices and the edge is going through edge runtime as well.

It is an extension of IoT Hub,  sitting on the devices. It also facilitates all communication between these modules, so these modules are talking to each other, they talk though  the runtime. The runtime is really responsible for doing that communication or making it happen, and based on our concept of routes so you essentially define routes with the edge runtime from the cloud, and it's implemented on the edge device.

All communication between the edge device and the cloud is done through edge runtime 



![Concept: IoT Edge runtime](/images/9_concept_runtime.png)



**How we bring these workloads onto the edge device?**

## Azure Iot Hub device management

![Concept: Device Management](/images/10_device_management.png)


There is a telemetry stream going from the device (on the left) to the cloud, and the cloud is sending comands to the IoT Edge. 
I show two arrows (logical arrows), that are an encrypted channel between IoT device and IoT hub. 

**Device twins** is the core concept here and it enables device management to happen. <br />
**Device twins** have two properties: **desired property and reported property**. <br />The **desired property** is owned by the cloud and can define what the desire property would be and that goes down to the IoT device, and the IoT device interprets that.<br/>
The **reported property** is owned by the device, and it is send up to the cloud.<br/>
Any time the IoT Hub in the cloud has the current state of the device (through the reported property) and any change. <br/>

These are the underlying mechanisms that we have in terms of Twins, which can use to configure IoT device today.

Now, this concept, we can apply it to the IoT edge device as well as the IoT Edge modules.

There are some other things also within a device management: they tag their methods, they job in queries  -i won't mention here-.. But really this is the core concept that we use for IoT Edge.

##IoT Edge in action
![IoT Edge in Action](/images/11_iotedge_in_action.png)

The blue rectangle is IoT Edge  (device) , with its SO (Windows or Linux).
Secure boot.

We have any kind of device, and when we put the IoT Edge Runtime, then it brings down the edge functionality on to this device.

The Operator selects which device is connected and which node in the device. <br/>
And then, in the cloud is deciding which workloads are needed to come down into the device (with Twins). Then the Edge runtime interprets the desired properties from the Twin and start pulling down these containers (that could be anything, any container based in workloads - Azure functions as stream analytics edge, ML, your own code…) 

The operator defines routes for these devices at these modules.
The routes are essentially when a message comes out from one module and it needs where it has to go. <br/>
Those routes are all defined in the cloud, in the device twin, then the routes come down and the edge runtime picks that up and starts the implementation.  <br />
Each module also has a twin in the cloud  and it brings down to the module (device). If we change a desired property in the twin, it will change in the edge module. 

**Device** => container workloads. <br />
**Routes** => in the cloud & control how messaging happens in the device<br />
**Module twin** => control define what kind of modules and parameters, and understanding what the state of each module is.<br />


Define in the cloud, how the edge device behaves (Configuration.)

**IP based device**: All the trafic can be routed from the edge device to different modules or send up to the cloud. <br />
If the device is **not an IP based device**, but it has bluetooth, you can put the BT module. It would be listening communication protocols (com port) and it would pick up all the data, and the module will become a proxy for that.
