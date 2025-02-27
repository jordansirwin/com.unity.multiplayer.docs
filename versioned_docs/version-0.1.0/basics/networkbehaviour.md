---
id: networkbehavior
title: NetworkBehaviour
---

[`NetworkBehaviour`](../mlapi-api/MLAPI.NetworkBehaviour.md) is an abstract class that derives from `MonoBehaviour` and is the base class all your networked scripts should derive from. Each [`NetworkBehaviour`](networkvariable.md) is owned by a [`NetworkObject`](networkobject.md). 

:::note
`GameObjects`, `NetworkObjects` and `NetworkBehaviour` aren't serializable types so they can't be used in `RPC`s or `NetworkVariables` by default. For infromation on how to send  a reference to a `NetworkBehaviour` over `RPC`s or `NetworkVariables` see [NetworkObject &NetworkBehaviour](../advanced-topics/serialization/networkobject-serialization.md).
:::

`NetworkBehaviours` can contain RPC methods and `NetworkVariables`. When you call an RPC function, the function isn't called locally. Instead a message is sent containing your parameters, the `networkId` of the `NetworkObject` that owns the `NetworkBehaviour` that the Invoke was called on, and the "index" of the `NetworkBehaviour` on the `NetworkObject`.
This means for multi project setups (one project for the server and another one for the client), it's important that the order and amount of `NetworkBehaviour`s on each `NetworkObject` is the same. It also means that `NetworkBehaviour`s can only exist as a child or on the same object as a `NetworkObject` that is actively Spawned.

You can have multiple `NetworkBehavior`s on the same object and on any child object. Each `NetworkBehaviour` belongs to a `NetworkObject`. It will be the first parent or first component on the current object that is found. You can only have one `NetworkObject` at the root of the prefab.

`NetworkStart` is called on each behavior related to the `NetworkObject`.

Inside a `NetworkBehaviour` you can use `NetworkVariable` and `RPC`s to synchronize state and send messages over the network.
