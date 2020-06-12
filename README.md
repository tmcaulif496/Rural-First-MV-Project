# Rural-First-MV-Project
Node-Red flow for the detection and alerting of animals/people/cars for farm welfare.

# Project Goals
The goal of this project initially was to use Meraki MV cameras to be able to detect badgers on a farm in order to decrease the possibility of cattle contracting tuberculosis. The project then expanded into more farm welfare related operations such as; Detecting vehicles that fly tip on the land; Detecting workers for their welfare, guests for sign in process, and detecting unwelcome intruders. After the completion of this project, the farm contact, Duncan has requested this project continue to be able to detect and identify cattle based off images.

# Project Requirements (versions)
Some of the requirements were as follows:

Functional requirements:
People Detection
Badger/Animal Detection
Vehicle Detection

Non-Functional requirements:
One central dashboard for ease of managment
Complexity hidden from customer side
Well structured flows for easy recreation and adjustement
Node-red prefered architecture 
Event based notification
Ease of integration with various farm technologies via APIs 


# High Level Design
The badger detection was achieved by using a combination of node-red, a flow based platform, microsoft's azure machine learning platform and the Meraki MV cameras and APIs. A flow is initiated in node-red when motion is detected and initates an API call to Meraki to take a snapshot. This snapshot is then sent to microsoft's azure platform, where a trained machine learning model designed to detect badgers exists. The model returns a percentage liklihood of a badger being in frame and this value is fed back into node-red. If the liklihood is above a chosen value a notification is sent to a custom made dashboard and stored.

The vehicle (registration plate) detection was achieved by using a combination of node-red, HiveMQ's public MQTT broker, open ALPR and the Meraki MV cameras and APIs. A flow is initiated in node-red when the MV camera detects a vehicle and then publishes a message to the MQTT broker which a node in node-red is subcribed to, thus initiating an API call to Meraki to take a snapshot. This snapshot is then sent to open ALPR to read the license plate. The image of the vehicle and the license plate along with the % confidence is sent to te node-red dashboard.


The people detection was achieved by using a combination of node-red, HiveMQ's public MQTT broker and the Meraki MV cameras and APIs. A flow is initiated in node-red when the MV camera detects a person and then publishes a message to the MQTT broker which a node in node-red is subcribed to. In the node-red dasboard a people meter/counter shows the number of people currently in the field of view of the camera.
