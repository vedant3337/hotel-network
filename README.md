# Hotel Network Design with VLAN Configuration and Internetworking

This project demonstrates the design of a hotel network in Cisco Packet Tracer with VLAN configuration and internetworking to ensure secure and efficient communication.

## Steps Followed

### 1. Physical Design
   - **Connection Type:** Use `copper-straight-through` for `switch-PC` connections and `copper-cross-over` for `switch-router` connections.

### 2. Enable Router Connections
   - **Action:** Enable the router’s wired connection by turning on the relevant port.

### 3. Connect Laptop to Access Point (AP)
   - **AP Configuration:**
     - Configure Port 1 of AP with SSID and WPA2 passphrase.
   - **Laptop Setup:**
     - Turn off the laptop, add a wireless gateway (`wpc300n`), then turn it back on.
     - Go to `Desktop -> PC Wireless`, connect to the `hotel-guest` network with password `guest@123`.

### 4. Add Floor 2 Devices
   - **Setup:** Added a second-floor switch, an AP, and guest laptops, then configured them accordingly.

### 5. DHCP Server Setup
   - **Action:** Add two DHCP servers, assigning each an IP and default gateway.

### 6. Assign DHCP IPs
   - **Action:** Assign DHCP IPs to all PCs on the network.

### 7. Router IP Configuration for Internetworking
   - **Action:** Assign IPs to both router ports, then configure static routing for internetworking.

### 8. DNS Server and HTTP Service Configuration
   - **Action:** Configure IP for the third network of the DNS server and edit the HTTP service on that server.

### 9. Configure West-Side DNS Server
   - **Action:** Set up the west-side server as the DNS server and reassign IPs to PCs as needed.

### 10. Configure Email Transfer
   - **Action:** Set up email transfer services within the network.

## VLAN Configuration

- **IP Assignment to Laptops:** Assign IPs to laptops based on VLAN requirements.
- **Switch Configuration for VLANs:**
  - Open VLAN database and add VLANs.
  - Set any non-end device ports as `trunk`.
  - Assign specific VLANs to end device ports.

- **Router VLAN Configuration Commands:**
  ```plaintext
  enable
  configure terminal
  interface f0/0.20
  encapsulation dot1Q 20
  ip address 192.168.20.1 255.255.255.0
  exit
  exit
  exit

## Access Control List (ACL) to Block Access of Guest from Employee and Server

- **Action:** Configure ACL on Router 1 to block guest VLAN (192.168.20.0/24) from accessing employee networks and the server.

- **ACL Configuration Commands:**
  ```plaintext
  enable
  configure terminal
  access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.60.2 0.0.0.0   // Deny access to server 60.2
  access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255   // Deny access to employee network 10
  access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255   // Deny access to employee network 30
  access-list 100 permit ip any any   // Permit access to all other networks
  interface f0/0.20
  ip access-group 100 in
