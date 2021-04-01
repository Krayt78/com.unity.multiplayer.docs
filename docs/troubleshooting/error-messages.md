---
id: errormessages
title: MLAPI Error Messages
---

Learn more about Unity error messages, including error collecting, issues that cause them, and how to handle.

## Error Capturing

Error messages are captured and returned through Unity Editor Diagnostics (required) and Roslyn Analyzers. ILPP occurs in Unity and returns error messages, which prevents you from building/playing your game (hard compile errors).

Roslyn Analyzers provide immediate feedback within the IDE, without jumping back to Unity to let it compile with your new changes. Unity ILPP and Editor errors are the source of truth.

## NetworkObject errors

**Error:** 
* `Cannot find pending soft sync object. Is the projects the same? UnityEngine.Debug:LogError(Object)`
* `ArgumentNullException: Cannot spawn null object  Parameter name: netObject`

This exception should only occur if your scenes are not the same, for example if the scene of your server contains a `NetworkObject` which is not present in the client scene. Verify the scene objects work correctly by entering playmode in both editors. This will add an `InstanceId` field to your `NetworkObject`s. These IDs should match on both projects.

## ServerRpc errors

**Error:** 
* Server: `[MLAPI] Only owner can invoke ServerRPC that is marked to require ownership`
* Host: `KeyNotFoundException: The given key was not present in the dictionary.`

The ServerRPC should only be used on the server. Make sure to add `isServer` check before calling.

If the call is added correctly but still returns a `nullreferenceexception`, `NetworkManager.Singleton` may be returning `null`. Verify you created the `GameObject` with a `NetworkManager` component, which handles all initialization. `NetworkManager.Singleton` is a reference to a instance of the `NetworkManager` component.

## NetworkVariable

**Error:**

Previous versions MLAPI 12.1.7 and older:
```
[MLAPI] Client wrote to NetworkedVar without permission. No more variables can be read. This is critical. NetworkId: 29 BehaviourIndex: 4 VariableIndex: 0
```

Unity MLAPI 0.1.0 and later:
```
[MLAPI] Client wrote to NetworkVariable without permission. No more variables can be read. This is critical. NetworkId: 29 BehaviourIndex: 4 VariableIndex: 0
```

A reference to the `NetworkVariable` (or `NetworkedVar` older versions) may not have a value correctly set. You can check through `NetworkVariable`s to locate which one attempts to set the value. 

The error message values help you locate the `NetworkVariable`:

* `NetworkId` indicates the object with that id. `NetworkId: 1` indicates and object with NetworkId 0.
* `BehaviourIndex` indicates the `NetworkBehaviour` (or `NetworkedBehaviour` older versions) at that position or order in the editor list. `BehaviourIndex: 0` is the first in the list.
* `VariableIndex` indicates the variable in that position or order in the `NetworkBehaviour` sorted by name. Sort the list of variables by name in the `NetworkBehaviour` and count down to that position in the list. `VariableIndex: 0` would be the first. 

## Connection Approval

**Error:**
The following error occured on MLAPI version 12.1.7 (may not occur in Unity MLAPI 0.1.0 or later) :

```
OverflowException: Arithmetic operation resulted in an overflow.
MLAPI.Serialization.BitReader.ReadByteArray (System.Byte[] readTo, System.Int64 knownLength) (at Assets/Third-Party/MLAPI/Serialization/BitReader.cs:781)
MLAPI.Messaging.InternalMessageHandler.HandleConnectionRequest (System.UInt64 clientId, System.IO.Stream stream) (at Assets/Third-Party/MLAPI/Messaging/InternalMessageHandler.cs:190)
MLAPI.NetworkingManager.HandleIncomingData (System.UInt64 clientId, System.String channelName, System.ArraySegment`1[T] data, System.Single receiveTime, System.Boolean allowBuffer) (at Assets/Third-Party/MLAPI/Core/NetworkingManager.cs:933)
MLAPI.NetworkingManager.HandleRawTransportPoll (MLAPI.Transports.NetEventType eventType, System.UInt64 clientId, System.String channelName, System.ArraySegment`1[T] payload, System.Single receiveTime) (at Assets/Third-Party/MLAPI/Core/NetworkingManager.cs:870)
MLAPI.NetworkingManager.Update () (at Assets/Third-Party/MLAPI/Core/NetworkingManager.cs:651)
```

This exception `(knownLength = -1)` happens if the client has connection approval deactivated in the `NetworkingManager` (`NetworkManager` in Unity MLAPI 0.1.0 and later) while the server has it activated. On the server side, MLAPI attempts to read the length of the connection approval array but fails due to the client not writing this into the stream at all.

To fix this issue, rebuild the client or server after activating Connection Approval in the `NetworkingManager` (or `NetworkManager`) should fix this issue.