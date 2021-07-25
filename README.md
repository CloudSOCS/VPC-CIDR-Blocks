VPC CIDR Blocks
---

CIDR (Classless Inter-Domain Routing) is a scheme to allocate Internet addresses used in inter-domain routing and Internet Protocol packets. Using CIDR a single IP address can be used to choose several unique IP addresses.

It assists routing by permitting blocks of addresses to be assembled into single routing table entries and these groups are commonly called as CIDR blocks which share an initial series of bits in the binary illustration of their IP addresses.

According to the CIDR standard, the first part of an IP address is a prefix, which identifies the network. The prefix is followed by the host identifier so that information packets can be sent to particular computers within the network.

We need to make sure we understand what CIDR block to use before we go there so that we make sure from the start that we're going to have enough subnets and enough hosts per subnet.So let's say we have a network address of 192.168.0.0. we have a 24 bit subnet mask and that gives us eight host bits, which is 256 addresses. The first address would be 0.1. The last address would be 0.254. The .0 address, so 192.168.0.0 is the network address. You can't ever use that for an IP address of a host. The last address would be 255. And you can't use that because that's the broadcast address.

![24 sub](/images/1.png)

Now, what if we have a /16 subnet mask? We have more than eight bits. We've got 16 bits for the host portion. And that gives us 65,536 potential addresses, minus the few that are reserved by AWS.

![16 sub](/images/2.png)

We don't have to stay in the boundaries of the octets themselves. We can have a variable length subnet mask. You can see here the subnet mask borrows four pieces from the host portion. So there's four bits used in the network portion and four bits of this particular octet used for the host bits, which gives 12 host bits. that means we get 4,096 addresses for that subnet.This is when we're using classless inter-domain routing with something called variable length subnet masks.

![sub16](/images/3.png)

Now there are a few rules and guidelines. Your CIDR block size can be between 16 and 28 AWS rules..The CIDR block must not overlap with any existing CIDR block associated with the VPC,And you can't increase or decrease the size of an existing CIDR block. If you then realize that you want to change the CIDR block because you've have reached some kind of limitation, it's going to be a real problem to do that. You'd have to migrate to another VPC.

Here are the address blocks you can get started with:
- 10.0.0.0 – 10.255.255.255 (10/8 prefix)
- 172.16.0.0 – 172.31.255.255 (172.16/12 prefix)
- 192.168.0.0 – 192.168.255.255 (192.168/16 prefix)

Let's use this tool that is on [network00.com](https://network00.com/NetworkTools/IPv4SubnetCreator/) website and it's the IPv4 Subnet Creater.
Put in 10.0.0.0. and I'm going to choose /16.
Mow we define the number of hosts or the number of subnets that we want to have. So I want at least 4,000 hosts in my subnets.That gives us lots of flexibility for the future.
![sub](/images/4.png)

 I'm going to choose create and it now shows us that it's recommending we use a /20 subnet mask for the subnets we create.

 ![create](/images/5.png)

 My CIDR block is going to be 10.0.0.0/16. My first subnet will be 10.0.0.0/20. My second subnet will be 10.0.16.0/20 And within each of these subnets ww have a maximum of 4,094 hosts minus the few addresses that are reserved by AWS. Next will be how to create our VPC.

