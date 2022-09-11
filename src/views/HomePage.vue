<template>home page...</template>

<script>
import { defineComponent } from "vue";

import mqtt from "mqtt/dist/mqtt";

var options = {
  host: "5359dba8b3e745a2b0f69e5c3b0f6ae7.s1.eu.hivemq.cloud",
  port: 8883,
  protocol: "mqtts",
  username: "anikethivemq",
  password: "fZD_VQ85#DC6A5u",
};

export default defineComponent({
  setup() {},
  mounted() {
    console.log(options);

    // initialize the MQTT client
    var client = mqtt.connect(options);

    // setup the callbacks
    client.on("connect", function () {
      console.log("Connected");
    });

    client.on("error", function (error) {
      console.log(error);
    });

    client.on("message", function (topic, message) {
      // called each time a message is received
      console.log("Received message:", topic, message.toString());
    });

    // subscribe to topic 'my/test/topic'
    client.subscribe("my/test/topic");

    // publish message 'Hello' to topic 'my/test/topic'
    client.publish("my/test/topic", "Hello");
  },
});
</script>
