# Repository for my notes
* Comet is an umbrella term, encompassing multiple techniques for achieving server to push data to a browser. Widespread support for WebSocket and server sent events has obsoleted the comet model.
* CometD is the reference client/server implementation of the Bayeux protocol, which defines messaging protocol for web clients to publish and subscribe to message channels.
* CometD provides a high level messaging service that makes it easy for webapp to publish messages to right users, without having to worry about network transports, disconnections, connection identities, etc. It is a scalable web event routing bus, that allows low-latency, server-side event-driven web applications.
* CometD uses transport independent protocol, the Bayeux protocol, that can be carried over HTTP or over WebSocket. It leverages WebSocket when it can, and uses Ajax push, when using HTTP.
* Information exchanged between client and server is a Bayeux message, formatted in JSON.
* The channel is a central concept in CometD. Publisher publish messages to channels and subscribers subscribe to channels to receive messages.
* All messages have a channel field.
* The Bayeux specification defines three types of channels. meta channels, service channels and broadcast channels.
* CometD creates meta channels. Applications cannot create new meta channels. This channel is used for information about Bayeux protocol. Such as whether handshakes are successful or not, whether connection is broken/re-estabilished.
* Applications create service channels, which are used for request/response style of communication. (not publish/subscribe);
* Applications also create broadcast channels. Which have the semantic of messaging topic and are used in the case of publish/subscribe style of communication. 
* CometD implements the hub-spoke topology.





