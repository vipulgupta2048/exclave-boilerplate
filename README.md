# Exclave Boilerplates

> A collection of opinionated boilerplates for exclave testing framework

Exclave is a factory test infrastructure written in Rust. Tests are designed to be easy to write in any language you care to, as Exclave will capture the output from your program and log it all. Once your test finishes, exit with a zero return code to indicate success or nonzero to indicate failure. More information & documentation can be informed on the [exclave repository](https://github.com/exclave/exclave)

## How to use boilerplates?

Each folder is a self-contained, atomic, and hot-swappable boilerplate to kickstart your first tests using Exclave. For easier deployment and execution of tests, a container environment is usually the preferred choice containing all the dependencies & libraries. For debugging, one can install Rust and build Exclave as well on the system. 

## Going over the boilerplate structure

Suppose you intend to run scripts or commands with Exclave. In that case, you need to make sure the path in the `WorkingDirectory` property of tests is stable and easily discoverable. Since editing tests is a hassle once you have many tests interlinking, this structure ensures readability while it is easier to debug. 

```
balena-exclave-boilerplate/
├── docker-compose.yml
├── exclave-control-center
│   ├── Dockerfile.template
│   ├── logic
│   │   ├── balenaSDK
│   │   ├── deviceSDK
│   │   ├── scripts
│   │   └── someOtherProgram
│   └── tests
│       ├── cli-testing.scenario
│       ├── quick-test.test
│       ├── raspberrypi.jig
│       ├── testing.scenario
│       └── trigger.trigger
├── some_other_service
└── testblockbot
```

The `exclave-control-center` container/service contains the tests directory containing exclave files. While the logic directory is to needed to support said tests containing scripts, programs, and other executables as required. Apart from this, `exclave-control-center` can include Dockerfiles, node_modules, package.json files, and more as the tests need. Exclave can be found in the `/usr/src/exclave` directory of the docker container while the rest of the files are copied in `/usr/src/core`. 

Exclave tests can be activated by running/SSH into the container and executing the command in the exclave directory. 

```
target/debug/exclave -c ../core/tests
```

According to the use case, one can also go the multi-container way and end up adding several other containers/services like Testblockbot, proxy servers, or other components as required. Containers can talk to each other through a bridged connection type and persist data in named volumes shared by one another. 

## Which boilerplate should work for you

1. **balena-exclave-boilerplate** - An exclave boilerplate ready to be built and used for popular embedded devices supported by balenaCloud with support for secrets, testblockbot, and adding other services.
2. **docker-exclave-boilerplate** - An exclave boilerplate ready to be built and used in containerized environments with support for adding new services and extending configurations as needed.   
2. **general-exclave-boilerplate** - An exclave boilerplate focused on test format and betters tests.
