# CS6110-project

*Raihan*

In this project, my goal was to verify the paho.mqtt.c and paho.mqtt.cpp protocol with frama-c. Following is my findings,

## Frama-C Installation
We initially attempted to install the Frama-C software analysis platform on MacOS but encountered unresolved dependency errors, leading us to switch to Ubuntu 20.04. Following the Frama-C's official installation guide, we faced an issue with the depext dependency due to its incompatibility with opam versions above 2.1.0. Attempts to downgrade opam were unsuccessful, and we eventually resolved the issue using opam-depext, an alternative method suggested in an online discussion thread. After resolving the dependencies and configuring the environment, we were able to successfully run Frama-C on a set of demo C programs.

## Connection Establishment
By invoking the client.connect(connOpts) method, a MQTT connection token (mqtt::token_ptr) with the name conntok is created. The code then uses conntok->wait() to wait for the connection to be established. It outputs "OK" following a successful connection to the MQTT server to show that the connection was successful.
![image15](https://github.com/mdrahmed/CS6110-project/assets/26908164/aa117f5d-b3d6-40f7-a721-9ea033e9c184)


## Subscription
It creates a MQTT subscription token (mqtt::token_ptr) with the name subtok.the method subscribe(TOPIC, 0).Subtok->wait() is then cSubscription: alled while the code waits for the subscription request to be recognized. It prints "OK" to show that the subscription to the topic was successful after it has been successfully completed.
![image12](https://github.com/mdrahmed/CS6110-project/assets/26908164/d43e2ce9-c5b1-4a91-90af-af11dd1806c9)


## Receiving Message
When the broker sends a MQTT message, this callback function is activated. The received message is represented as a MQTT message object via the field msg, which is a required input. The snippet of code uses msg->get_topic() to print the subject of the message that was received. Additionally, it uses msg->to_string(), which represents the message payload as a string, to print the message's contents.
![image4](https://github.com/mdrahmed/CS6110-project/assets/26908164/4435a901-a6c6-4234-98da-a8c15bc5f88a)


Following image verifies that the client subscribed to the topic appropriately,
![image1](https://github.com/mdrahmed/CS6110-project/assets/26908164/8ef272bb-3954-47b8-b637-c436bdbab297)


## Publishing message
The message content to be sent, in this example "Hello, MQTT!" has been set in the  publishing phase by initializing a string variable called payload. Using the mqtt::make_message() function, it generates a MQTT message pointer (mqtt::message_ptr) with the name pubmsg. The subject to which the message will be published is specified by the subject argument, and the payload is designated as the message's body. Using pubmsg->set_qos(0), the code reduces the Quality of Service (QoS) level for the message to 0. QoS 0 denotes that the message will only be transmitted once and does not call for the recipient's acknowledgement.By dialing, it publishes the message to the MQTT broker. The message is sent to the broker for delivery using the publish() method. Before moving on to the next line of code, the wait() method makes sure that the publishing procedure has finished. 

![image5](https://github.com/mdrahmed/CS6110-project/assets/26908164/1caec56e-425e-4bdc-8892-a8ecdbf0b258)

Following image verifies that the client and publisher is able to receive and send message with the broker,
![image18](https://github.com/mdrahmed/CS6110-project/assets/26908164/ab2dbced-51b6-4b3f-a101-caff3609cb92)


## Verifying with frama-c
On the file "Messages.c," we ran the Frama-C analysis using the Eva plugin with an accuracy level of 3, and we came to the conclusion that there were no mistakes. An extensive review of the code, including loop unrolling, widening delay, subdomain thresholds, and other Eva setup settings, was done during the analysis. We made sure a thorough assessment of the behavior of the code by designating the entry point function as main in the analysis command. The lack of any detected faults suggests that the "Messages.c" code is secure and adheres to the defined analysis settings.
![image20](https://github.com/mdrahmed/CS6110-project/assets/26908164/22bd831d-f74e-485b-8fe9-442c07c208bc)


We used Frama-C to analyze the "MQTTAsync.h" and "MQTTAsync.c" files and discovered no bugs or vulnerabilities. To ensure a thorough evaluation of the MQTT asynchronous library implementation, the analysis was carried out using the Eva plugin with default precision settings.
![image14](https://github.com/mdrahmed/CS6110-project/assets/26908164/04d2bfc7-2342-4120-bb4a-15da1c62349a)


After verifying the paho.mqtt.c libraries when we tried to use Frama-C to check the message.h file in the paho.mqtt.cpp library, we ran into a dependency problem. That prevented us from carrying out the needed verification. It appears that the analysis may be hindered by unresolved dependencies or a lack of necessary libraries. Before doing the verification again, we advise addressing the dependency issue and making sure that all required libraries and dependencies are correctly installed.
![image9](https://github.com/mdrahmed/CS6110-project/assets/26908164/89a3c4df-3256-4608-b96a-abee84117b5b)



