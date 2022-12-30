---
title: 'How we made it'
date: 2019-02-11T19:27:37+10:00
weight: 2
---

### System diagram:

![sys](/sys.png)

Components list:

| Component Name| Quantity |
| ------------- | ------------- |
| car chassis | 1  |
| servo motor | 1  |
| DC motor  | 2  |
| motor driver | 1 |
| joystick | 1 |
| sound sensor  | 1  |
| distance/motion sensor  | 1|
| voltage switch  | 1|

### Development
Attached below is the proposed idea of Wrangler(which is a bit different from the final deliverable). The proposed model is cute and interesting. We were thinking using a motion sensor APDS9960 to control the Wrangler to move in different directions. 

![image](https://user-images.githubusercontent.com/84453030/209241315-e3d71c71-575d-415a-b744-bcac83668311.png)

First thing we did was to plan the use of the pins of the QT PY 2040 board. We read through the datasheet and allocated the pins and memories for different uses. The pins are assigned as below:

{{< figure src="/pins2.jpeg" alt="dwarf" width="400px" class="content-gallery" >}} {{< figure src="/pins1.jpeg" alt="dwarf" width="400px" class="content-gallery" >}} 

We started from making each small module work and then combined them altogether. They can be summarized as 
![logic](/logic.png)

After coding, configuring, testing all the broke-down functions mentioned, we mounted them onto the chassis. The breadboard was secured on the first layer of acylic board on the chassis, the wires were carefully arranged for clarity and ease of debugging. The second layer of acrylic board was used hold the "wrangler" toy for a better visual prospective.
{{< figure src="/mount.png" alt="dwarf" width="800px" class="content-gallery" >}} 

Then we tried to test the functions in an integrated manner by redesigning the C file, Cmake files and code structures. After failing due to a few bugs, we managed to get functions working. However, there are still structural problems that we found out during the process. The wrangler was placed too high and when the motors drive the chassis to move, especially forward,  the Wrangler loss balance. Thus, we decided to implement some weights at the bottom layer to lower the center of gravity and adjusting the running interval of motor for a smoother movement. 

The final deliverable looks like this: 
{{< figure src="/finallook.png" alt="dwarf" width="800px" class="content-gallery" >}} 



