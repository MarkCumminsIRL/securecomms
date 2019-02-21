# Lab 5: Arp Spoofing/Poisoning

In this lab we will create a small switched network and attempt to perform some network sniffing/eavesdropping. 

___

## Lab Contents

1. Our Network Set-up
2. Attempting to intercept traffic
3. Eavesdropping on other peoples traffic
4. Enabling Port Forwarding
5. Arp Spoofing Summary

___

### Our Network Set-up

For this lab you will need 3 machines connected to a single switch. Two of the machines will communicate with each other while the attacker on a third machine attempts to listen-in on their communications.

The fist two machines (A & B) may be any VM or physical machine you wish, lets use the following IPs to keep it easier.

A. 192.168.1.10
B. 192.168.1.20
C. 192.168.1.100

Cable up our network and ensure we can ping between all machines. Don't move on until this is working correctly between all devices.

### Attempting to intercept traffic

OK so once we have our network set up we will attempt to capture traffic between A-B from our attackers machine, C

We will also use the lab as an excuse to look at some new tools also. We will start by attempting to use TCPDUMP to record the traffic and we can then view it in more detail using Wireshark.

To install both tools on ubuntu we can use the following commands.

```bash
sudo apt install tcpdump -y
```

```bash
sudo add-apt-repository ppa:wireshark-dev/stable
sudo apt-get update
sudo apt-get install wireshark
```

Once installed we should be good to begin intercepting traffic. So lets start pinging between A and our attacker C, just to check we are capturing traffic. On our attacking machine we can begin capturing traffic using the following command.

```bash
sudo tcpdump -i interface_name -w capture1.pcap
```

Once we have captured some traffic we can close the recording and open our captured traffic with wireshark and we should see our icmp ping traffic between A and C.

```bash
wireshark capture1.pcap
```

### Eavesdropping on other peoples traffic

In the previous example we were able to record and capture traffic because we were part of the communication and the traffic was sent to or from ourselves. If we wanted to record traffic between other users that didn't involve us then we get a problem. On a fully switched network the switch only routes traffic where it needs to go so since we are not part of the conversation the switch doesn't send any traffic our way so there is no way for us see or capture the traffic.

Try it. Start capturing traffic again but this time only send traffic between A - B, if your network is set up correctly then we shouldn't see any traffic from the pings recorded in our capture.

To get a round this problem we will attempt to use arp spoofing and trick the other users into sending their traffic to us. There are plenty of tools we can use for this but for this lab we will attempt to use the arpspoof, part of the dsniff tools.

```bash
sudo apt install -y dsniff
```

The following command will tell the A “I am 192.168.1.20” or B, and the next command tells 192.168.0.20 or B “That I am A”

```bash
sudo arpspoof 192.168.1.10 -t 192.168.1.20
sudo arpspoof 192.168.1.20 -t 192.168.1.10
```

You'll need to run each spoof command in a separate window as it stays active sending fake arp replies to each of our targets.

Once complete attempt to capture the traffic as above, between A and B, ensure you are pinging between A and B and vice-versa.

#### Enabling Port Forwarding

Hopefully our arp spoofing worked and you can now see traffic that is being sent between other users on our network and we can run a person in the middle eavesdropping attack on their traffic.The eagle eyed among you may have spotted a problem. When we send our pings now we aren't getting any responses anymore. The reason for this is that we have directed all traffic to ourselves but we haven't told our own machine to forward on this captured traffic as normal so that it gets to its intended destination. so to complete our attack we should enable port forwarding for all traffic we have diverted to ourselves.

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

Now if we rerun the earlier experiment we should be able to see traffic and the pings response rate should also be normal as traffic is being rerouted correctly.

#### Arp Spoofing Summary

In future assuming you have the tools installed now,  we just need to run the following commands to carry out our arp spoofing attack.

```bash
sudo arpspoof IP_A -t IP_B
sudo arpspoof IP_B -t IP_A
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward  
```

#### Arp Spoofing Challenge Exercise

Ok so we've used the arpspoof tool to carry out a simple person in the middle eavesdropping attack. But can you create your own tool to do the same?

Essentially we just need to repeatedly send arp replies to our target with fake mac addresses, ie. our mac in place of the other machine.

We can use scapy with our python code to help do most of the work.. check out scapy to see how to get it todo what we need.Try the small snippet of code given.

```python
from scapy.all import *
target = "192.168.1.10"
print(sr1(IP(dst=target)/ICMP()),timeout=2)
```
