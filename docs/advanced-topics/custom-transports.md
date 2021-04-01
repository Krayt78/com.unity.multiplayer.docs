---
id: custom-transports
title: Custom Transports
---

The MLAPI uses Unity’s [UNet Transport Layer API](https://docs.unity3d.com/Manual/UNetUsingTransport.html) by default and has support for custom Transports. 

A Transport collects messages from the application and transmits them over the network. 
The Transport layer is also responsible for making sure that all packets arrive and that they arrive in order if needed. Transports also make sure that your data won't get corrupted when it's sent over the network.

MLAPI always works in a client-server or client-host model; a transport cannot change that. Transports are available for nat punching or transfer your data over a relay. The [SteamP2P transport](https://github.com/Unity-Technologies/mlapi-community-contributions/tree/master/Transports/com.mlapi.contrib.transport.steamp2p) is an example that uses the Steamworks network to transfer your data and allows clients to connect to each other without needing to open ports on the host machine.

## Community Contribution

The MLAPI supports community contributions for Transport implementations. See the [MLAPI Community Contributions](https://github.com/Unity-Technologies/mlapi-community-contributions)  repository to learn more.

## Install and Use Transport

See the [MLAPI Community Contributions - Transports](https://github.com/Unity-Technologies/mlapi-community-contributions/tree/master/Transports) repo to see a list of available transports.

To use a Transport, follow the [Community Transport Installation Guide](https://github.com/Unity-Technologies/mlapi-community-contributions/blob/master/Transports/README.md).

## Writing Your Own

To get started writing Transport interfaces, the current implementations for UNet Transport Layer API, ENET, and Ruffles are good starting points for learning their flow. If you write a wrapper for a well-known Transport, please open a PR to add it to the [MLAPI Community Contribution repository](https://github.com/Unity-Technologies/mlapi-community-contributions).

## Adding New Content

Check our [contribution guidelines](https://github.com/Unity-Technologies/mlapi-community-contributions/blob/master/CONTRIBUTING.md) for information on how to contribute to the MLAPI Community Contribution repository.
