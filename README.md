# ExpressRoute--What-is-this NextHop-IP?

# Intro
Many users have provisoned an expressRoute circuit, dumped the affective routes of a VM in a VNET attached to the circuit, and seen this mysterious IP as next hop! So what is this IP address? This IP is perfectly normal even though it's not in any subnet or network you provisoned, so what is this address? This is the IP address of the Azure MSEE, the physical IP. Normally you would see two, one for the primary MSEE and one for the secondary MSEE if you have both primary and secondary VRFs up for the circuit. In this simple lab for illustration purposes, I only provisoned the primary path, so one MSEE on my circuit.

# Simple Topolgy
![image](https://user-images.githubusercontent.com/55964102/219828123-95a06026-9ce7-4f31-abe9-0bda0a52024c.png)

Dumping the effective routes of the hubVM or either spoke vms, we see this IP has next hop....taking our SpokeVM for example:
![image](https://user-images.githubusercontent.com/55964102/219828225-9121f5c8-3639-4c7d-bfcc-323a8c08a4a9.png)

So we can see from SpokeVM, it has learned GCP VPC of 192.168.0.0/24 and it also knows about the /30 interface we provisoned for ExR, in this case the primary which is 10.4.1.0/30. The next HOP to both of those addresses is the MSEE physical IP.
![image](https://user-images.githubusercontent.com/55964102/219828289-2c522540-25d8-48dc-97b9-274ebe051c53.png)

# Conclusion
We can conclude that this IP is normal and part of the ExpressRoute provision process. In a future date, we are looking to add this to our public documenation to avoid confusion and alarm. 

