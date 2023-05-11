# CS6110-project
In this project, we will verify MQTT libraries using advanced static analysis and symbolic execution tools. We are verifying the following MQTT libraries:

- Paho MQTT C++ Client: [https://github.com/eclipse/paho.mqtt.cpp](https://github.com/eclipse/paho.mqtt.cpp)
- MQTT-C: [https://github.com/LiamBindle/MQTT-C](https://github.com/LiamBindle/MQTT-C)

Our verification process is divided into three parts, each deploying a unique verification approach on specific components of the libraries. These three parts are implemented by Raihan Ahmed, Levi Li, and Yu Pan respectively. We are using the following tools:

- Raihan Ahmed: Frama-C
- Levi Li: CSeq
- Yu Pan: KLEE

