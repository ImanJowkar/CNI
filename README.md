# What is CNI(Container Network Interface)
Of course! CNI, which stands for Container Network Interface, is a set of rules that help containers (like those you create with Docker or Kubernetes) talk to each other and the outside world.

Imagine you have different types of containers, each needing to share information or stay separate. CNI is like a special instruction manual that helps these containers set up their communication system in a consistent way.

It's like having different gadgets that need to connect to the internet. CNI is the standard way to plug them in so they can work together without causing confusion. This makes it easier to manage and control how containers talk to one another and the rest of the digital world.

## Docker Networking:
Docker supports several types of networks that you can use to control how containers communicate with each other and the outside world. Here are some of the commonly used network types in Docker:

* `Bridge Network`:
This is the default network mode in Docker. It creates a private internal network on your host machine, and each container connected to the bridge network can communicate with other containers on the same network. Containers on the bridge network can also communicate with the external network through Network Address Translation 


* `Host Network`: 
In this mode, containers share the host machine's network stack. This means that containers directly use the host's network interfaces and do not have network isolation from the host or other containers. It can offer slightly better performance but less isolation.

* `Overlay Network`:
 This type of network is used for container communication across multiple Docker hosts or nodes. It's commonly used in orchestration systems like Docker Swarm or Kubernetes to enable containers on different hosts to communicate seamlessly as if they were on the same network.

* `Macvlan Network`: Macvlan allows containers to have their own MAC addresses and appear as separate physical devices on the network. This can be useful when you want containers to be directly reachable on the network, as if they were physical devices.

* `None Network`: Containers attached to this type of network have no networking interfaces configured. They can't access the network by default. This can be useful in scenarios where you want to isolate a container completely from any network communication



## some terminology:
Before we compare take a look at the available CNI plugins, it’s helpful to go over some terminology that you might see while reading this or other sources discussion CNI.
* `Layer 2 networking`:
Layer 2 networking, also known as data link layer networking, is a fundamental concept in computer networking that involves the second layer in the OSI (Open Systems Interconnection) model. This layer is responsible for establishing communication between devices on the same physical network segment, such as Ethernet or Wi-Fi, through the use of MAC addresses.Imagine you're in a big building with lots of rooms, and each room has a nameplate outside the door. This nameplate is like a "MAC address," a unique ID for every device (like a computer or phone) that wants to talk to others.
Now, let's say you want to send a letter to your friend who is in a different room. You put the letter in an envelope (this is your data) and write your friend's room name (MAC address) on the front.
A "switch" is like a helpful mail sorter in the building. It reads the room names (MAC addresses) on the envelopes and figures out which room each letter should go to. It makes sure the letters only go to the right rooms, not all over the place.
This sorting and sending of letters (data frames) between rooms (devices) is what we call Layer 2 networking. It's like a smart system that helps devices communicate directly with each other on the same "floor" of the building (local network), using their unique room names (MAC addresses).
So, in simple terms, Layer 2 networking is like sending messages (data) to different rooms (devices) in a building using their room names (MAC addresses) with the help of a mail sorter (switch) that makes sure everything goes to the right place.

* `Layer 3 Networking`:Imagine you have a big city with lots of streets and buildings. Each building has an address, kind of like a "IP address," which is a unique number for every device (like a computer or a printer) connected to the network.
Now, let's say you want to send a package to your friend's house in another part of the city. You put the package in a delivery truck and write your friend's building address (IP address) on it.
A "router" is like a smart traffic guide in the city. It looks at the building addresses (IP addresses) on the packages and figures out the best routes to take. It ensures the packages reach the correct buildings by following the right roads (routes).
This guiding and sending of packages (data packets) between buildings (devices) in the city (network) is what we call Layer 3 networking. It's like a system that helps devices communicate not just within the same neighborhood (like in Layer 2) but across the whole city (network), using their building addresses (IP addresses) and the help of routers.
So, in simple terms, Layer 3 networking is like sending packages (data) across different buildings (devices) in a city (network) using their building addresses (IP addresses) with the assistance of traffic guides (routers) that ensure everything reaches the correct destination.

* `VXLAN(Virtual eXtensible Local Area Network)`:
Imagine you have a magical tunnel that connects different houses in a village. Each house has a unique color, like a special code, so you know which house belongs to whom. Now, let's say you want to send gifts or messages to friends who live in other houses, even if they are far apart. You put your gift in a box and wrap it with a special colored paper (like the color of your friend's house).VXLAN is like creating these magical tunnels and special colored papers for your gifts. It helps your messages travel between houses, even if they're not right next to each other. This way, you can easily talk to friends in any house using your secret colors (VXLAN IDs), and they will receive your gifts through these magical tunnels.
So, in simple words, VXLAN is like sending special colorful packages (data) between houses (computers or devices) using magical tunnels (virtual network) so that you can talk to faraway friends as if they were close by.


* `BGP (Border Gateway Protocol)`: Imagine you're a traveler and you want to know the best route to get from one city to another. You ask people for directions, but you trust the most experienced travelers who know the roads really well.
BGP, which stands for Border Gateway Protocol, is like a super-smart guide for the internet. It helps different parts of the internet (called networks) know the best paths to send data from one place to another. Just like you trust experienced travelers, BGP helps networks trust each other's directions.
When a network wants to send data to another network, BGP helps decide which paths are the quickest and safest. It's all about making sure data takes the fastest and most reliable routes, just like you would when traveling.
So, BGP is like a digital travel guide that helps networks find the best roads (routes) for sending data across the vast landscape of the internet.




