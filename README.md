# SDN Firewall using POX and Mininet

## Problem Statement

The objective of this project is to implement a Software Defined Networking (SDN) based firewall using Mininet and the POX OpenFlow controller. The firewall enforces traffic control policies by installing flow rules in the switch.

---

## Objectives

* Demonstrate controller–switch interaction
* Implement flow rule design using match-action logic
* Observe network behavior for allowed and blocked traffic

---

## Technologies Used

* Mininet
* POX Controller
* Python
* Open vSwitch (OVS)

---

## Setup and Execution Steps

### 1. Clean Mininet

```bash
sudo mn -c
```

### 2. Run POX Controller

```bash
cd ~/pox
./pox.py log.level --DEBUG ext.firewall
```

### 3. Run Mininet (in a new terminal)

```bash
sudo mn --topo single,3 --controller=remote,ip=127.0.0.1
```

---

## Firewall Rules Implemented

* Block traffic from IP address: 10.0.0.1
* Block traffic from MAC address: 00:00:00:00:00:01
* Block TCP port: 80 (HTTP)
* Allow all other traffic

---

## Controller Logic

* Uses the `ConnectionUp` event to install flow rules in the switch
* Uses a `PacketIn` handler to process incoming packets
* Applies match-action rules using OpenFlow

---

## Testing and Validation

### Blocked Traffic

```bash
mininet> h1 ping h2
```

Result: 100% packet loss

---

### Allowed Traffic

```bash
mininet> h2 ping h3
```

Result: Successful communication

---

## Flow Table Verification

```bash
sudo ovs-ofctl dump-flows s1
```

The flow table shows:

* Drop rule for specific IP address
* Drop rule for specific MAC address
* Drop rule for TCP port 80
* Default rule to allow other traffic

---

## Results

The firewall was successfully implemented and tested.
The system correctly blocks and allows traffic based on defined rules.
Flow table entries confirm that rules are installed and enforced by the switch.

---

## Conclusion

This project demonstrates how SDN enables centralized control of network behavior.
Using POX and OpenFlow, firewall policies can be implemented efficiently and applied dynamically at the switch level.

---

## Author

Sreyaesh Peruri
