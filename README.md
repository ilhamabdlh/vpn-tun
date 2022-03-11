# vpn-tun

## under construction

- VPN Tunnel is almost built here,
after telnet, I try to build a VPN network with same specs as Telent. i.e. having 1 server to control the clients, and each client must be connected to server so that they can communicate with each other.
i use the library "github.com/songgao/water" for build tunnel.

## Topology
![topology](https://user-images.githubusercontent.com/72017753/157837323-f2e74636-de9f-42dd-be21-fd2a953df9fa.png)

Im trying to build a network with VPN Tunnel, let's look the topology, there is a server is the control for networks that will communicate. In topology, I set PC B as a server to control the connection between clients. Then, and I set PC C to be Client1, I liken PC C to Atop device. and I set PC A to be Client2, as a User who want to access the device.

## usage

- first type in the command prompt "PC B" as a server.
```sh
go run main.go -s -l=:3001 -c=192.168.254.169/24 -k=123456
```
"-s" flag for server,
"-l" http port
"-c" vpn ip and port
"-k" key (must be the same on server and client)

 ![Server](https://user-images.githubusercontent.com/72017753/157834000-a2f82501-a4a9-4c2b-bc47-2c019322a783.PNG)
 
 above is a description of server, on port 3001 is the port to open an http network. can be directly seen on "127.0.0.1:3001",
 
![home](https://user-images.githubusercontent.com/72017753/157834282-24a3485c-00df-42ba-ab4c-8d9d649a4a63.PNG)

next, we will make a connection between the client and server. type:
```sh
go run main.go -l=:3000 -s=server-addr:3001 -c=172.16.0.10/24 -k=123456

```
![client](https://user-images.githubusercontent.com/72017753/157834971-ad8e1327-f9d7-40a2-b943-d1c5fc66df67.PNG)

and then, you can see in "127.0.0.1:30001/register/list/ip", those are some clients that have been connected by server.

![list_user](https://user-images.githubusercontent.com/72017753/157835349-aa9c5ea5-e54a-402a-8f1f-75b21a1c87f6.PNG)

## TODO:
- cant communicate with each other between clients
- do handshake with a more secure key
- create a room so that intended user and device can communicate with each other
- deploy servers to cloud, they can be used on different networks

