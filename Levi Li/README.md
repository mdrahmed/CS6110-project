# CS6110-project

*Levi Li*

In this project, my goal is to verify function `mqtt_sync` (in `mqtt.c`) using CSeq framework. The `mqtt_sync` function is responsible for handling message acknowledgments, resending messages, and managing the keep-alive mechanism. I created a multi-threaded wrapper (in `wrapper.c`), since MQTT-C is a single-threaded library, while CSeq is a framework for checking concurrent C programs.

Files:
- `mqtt.c`, `mqtt.h`, `mqtt_pal.c`, `mqtt_pal.h` are MQTT libraries from [https://github.com/LiamBindle/MQTT-C](https://github.com/LiamBindle/MQTT-C)
- `wrapper.c` is a multi-threaded wrapper used for testing the `mqtt_sync` function
- `_cs_wrapper.c` and `_cs_wrapper.c.c1.from0to0.log` are the output of CSeq
