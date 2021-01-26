# Testbotblock

To use, 

1. Add the following to your docker-compose, and deploy

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

2. Add configuration to balenaCloud app. 

```
applicationConfigVariables:
    - BALENA_HOST_CONFIG_core_freq: "250"
    - RESIN_HOST_CONFIG_dtoverlay: "\"balena-fin\",\"uart1,txd1_pin=32,rxd1_pin=33\""
```

3. Server should start at http://localhost:5001, access it by making GET requests with endpoints listed in the index.js file. 
