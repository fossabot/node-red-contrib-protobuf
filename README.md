# node-red-contrib-protobuf
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fw4tsn%2Fnode-red-contrib-protobuf.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fw4tsn%2Fnode-red-contrib-protobuf?ref=badge_shield)


This project features protobuf encode/decode nodes. Load a proto file, supply a desired type for encoding or decoding and have fun.

## Installation

To install run

```bash
npm install node-red-contrib-protobuf --production
```

Omit the `--production` flag, in order to install the development dependencies for testing and coverage.

This node depends on protobufjs as the main package and will install it along with it.

## Usage

1. Grab a `proto` with the message types required
2. Place an encode/decode node on a flow
3. Open the editor and add a new protofile configuration node
4. Supply the path to your `.proto` file
5. Either supply a proto type
    1. within the encode/decode configuration
    2. with the `msg.protobufType` field (takes precedence over node configuration)

*Note on the protofile node* If the file contents of the `.proto`-file change on disk, a redeploy of the config node is necessary since it does not track changes on the file system or reload the file on every incoming message.

## Contribution

To setup your local development environment first clone this repository and then use docker to get your node-red environment up and running like this:

```bash
sudo docker run -p 1880:1880 --privileged -v $PWD:/tmp/node-red-contrib-protobuf -d --name nodered nodered/node-red-docker
```

After you saved your changes to the code update the installation within the container with this command:

```bash
sudo docker exec -u root -it nodered npm install /tmp/node-red-contrib-protobuf/ && sudo docker restart nodered
```

*Note on `--privileged` and `-u root`*: This is mostly required on linux machines with SELinux to avoid permission errors. Keep in mind that this is insecure and considered real bad practice. Alternativly configure your SELinux to allow access from the container to the local mounted volume in order to install the npm dependencies.

### Testing and Coverage-Report

First `npm install` for the dev dependencies. Tests, linting and code coverage are then available through:

```bash
npm test
npm run coverage
npm run lint
```

## License

The BSD 3-Clause License

[Alexander Wellbrock](https://w4tsn.github.io/blog)


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fw4tsn%2Fnode-red-contrib-protobuf.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fw4tsn%2Fnode-red-contrib-protobuf?ref=badge_large)

## Roadmap

* validate type from loaded .proto files
* allow `.proto`-path to be a URL
* expose more configuration parameters from the protobufjs API
* write tests covering misconfiguration and errors/exceptions