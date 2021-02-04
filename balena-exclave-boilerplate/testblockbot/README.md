# Testbotblock

To use the testbotSDK block, follow the steps below. 

> FOR INTERNAL USE ONLY

0. Assemble your [testbot](https://github.com/balena-io/testbot/blob/master/documentation/getting-started.md#assemble-a-standalone-testbot-machine), flash the [firmware](https://github.com/balena-io/testbot/blob/master/documentation/getting-started.md#provision-the-testbot) and [test](https://github.com/balena-io/testbot/blob/master/documentation/getting-started.md#test-if-the-testbot-is-functioning) if the testbot works and is ready to go. When complete your testbot is now ready to for you to work, move your device to the application as per your usecase.

1. Add the following to your docker-compose and deploy it with your application. The named volume `os-images` is where the testblockbot looks for images to flash onto the DUT. Do make sure the image is present here before you trigger the `/flash` endpoint. 

```
version: '2'

volumes:
  os-images:

services:
  testblockbot:
    image: balenablocks/testblockbot:latest
    privileged: true
    restart: always
    volumes:
      - os-images:/images
    expose:
      - "5001"
    environment: 
      - DBUS_SYSTEM_BUS_ADDRESS=unix:path=/host/run/dbus/system_bus_socket
```

2. Add the fleet configuration variables to your balenaCloud application

```
applicationConfigVariables:
    - BALENA_HOST_CONFIG_core_freq: "250"
    - RESIN_HOST_CONFIG_dtoverlay: "\"balena-fin\",\"uart1,txd1_pin=32,rxd1_pin=33\""
```

3. Server should start at `testblockbot:5001` and can be accessed by making GET requests with endpoints listed in the index.js file. Logs & request response can be observed from the `testblockbot` service on your application's balenaCloud dashboard. 

## Documentation for TestbotSDK 

Check out the steps for generating [TestbotSDK documentation](https://github.com/balena-io/testbot/tree/master#generating-documentation-for-testbotsdk).

## License 

All source code under Apache License v2.0
