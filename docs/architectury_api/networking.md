---
layout: page
title: Networking
parent: Architectury API
nav_order: 4
---

# Networking
{: .no_toc }

---

There are currently a few ways to setup networking with Architectury API:

- [Receiver Callback (Fabric-Like)](#receiver-callback)
- [Message Channel (Forge-Like)](#message-channel)

## Differences between Server and Logical Server

When you join a world in singleplayer, Minecraft fires a local integrated server. This is to separate the client and the server (logical server) logics, and to allow Opening to LAN.

# Receiver Callback

Each type of message is differentiated by a `ResourceLocation`, start by statically declaring one, so we can use it later.

```java
public static final ResourceLocation EXAMPLE_PACKET_ID = new ResourceLocation("examplemod", "example_packet");
```

## Registering the Handler

Now, depending on the direction of the transmission, we will register the packet receiving handler in a different location.

#### Client -> Logical Server

When we send a packet from the client to the server, we will register the handler on the common side.

#### Logical Server -> Client

When we send a packet from the server to the client, we will register the handler on the client side.

```java
// We are using S2C here for an example, use C2S instead if this is from the client to the server
NetworkManager.registerReceiver(NetworkManager.Side.S2C, EXAMPLE_PACKET_ID, (buf, context) -> {
    Player player = context.getPlayer();
    // Logic
});
```

## Sending the Packet

#### Client -> Logical Server

```java
FriendlyPacketBuf buf = new FriendlyPacketBuf(Unpooled.buffer());
NetworkManager.sendToServer(EXAMPLE_PACKET_ID, buf);
```

#### Logical Server -> Client

```java
FriendlyPacketBuf buf = new FriendlyPacketBuf(Unpooled.buffer());
NetworkManager.sendToPlayer(player, EXAMPLE_PACKET_ID, buf);
```

## Handling the Packet

The packet buffer supplied is a stream of bytes sent over the network, you must read it in order of how you sent it.

Let say, we want to send a block position and an item stack to the server. In between creating the packet buf and sending it, we can write our data to it.

```java
FriendlyPacketBuf buf = new FriendlyPacketBuf(Unpooled.buffer());
buf.writeBlockPos(pos);
buf.writeItem(stack);
NetworkManager.sendToServer(EXAMPLE_PACKET_ID, buf);
```

And then on the server, we can read it.

```java
NetworkManager.registerReceiver(NetworkManager.Side.C2S, EXAMPLE_PACKET_ID, (buf, context) -> {
    BlockPos pos = buf.readBlockPos();
    ItemStack stack = buf.readItem();
});
```

# Message Channel

First, we need to register a message channel for our packets to go through.

```java
public static final NetworkChannel CHANNEL = NetworkChannel.create(new ResourceLocation("examplemod", "networking_channel"));
```

Then, we will create a message class like this:

```java
public class ExampleMessage {
    public ExampleMessage(FriendlyPacketBuf buf) {
        // Decode data into a message
    }
    
    public ExampleMessage() {
        // Message creation
    }
    
    public void encode(FriendlyPacketBuf buf) {
        // Encode data into the buf
    }
    
    public void apply(Supplier<PacketContext> contextSupplier) {
        // On receive
    }
}
```

After this, we will register the message into the channel.

```java
CHANNEL.register(ExampleMessage.class, ExampleMessage::encode, ExampleMessage::new, ExampleMessage::apply);
```

## Attaching more data with the message

For any data we want to add to the message, we will want to add fields, then add logic to encode, and decode it over the network.

Let say, we want to send a block position and an item stack to the server.

```java
public class ExampleMessage {
    public final BlockPos pos;
    public final ItemStack stack;
    
    public ExampleMessage(FriendlyPacketBuf buf) {
        this(buf.readBlockPos(), buf.readItem());
    }
    
    public ExampleMessage(BlockPos pos, ItemStack stack) {
        this.pos = pos;
        this.stack = stack;
    }
    
    public void encode(FriendlyPacketBuf buf) {
        buf.writeBlockPos(pos);
        buf.writeItem(stack);
    }
    
    public void apply(Supplier<PacketContext> contextSupplier) {
        // Do logic here
    }
}
```

