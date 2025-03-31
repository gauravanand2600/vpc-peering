# VPC Peering Setup

## Overview
This setup demonstrates a VPC Peering connection between two AWS Virtual Private Clouds (VPCs), allowing instances in one VPC to communicate with instances in another. The architecture consists of:

- **Test-VPC-01** (Public Subnet) with an EC2 instance
- **Test-VPC-02** (Private Subnet) with an EC2 instance
- **VPC Peering Connection** enabling routing between the VPCs
- **Internet Gateways** for external connectivity
- **Routing Tables** ensuring proper network traffic flow
  ![vpc drawio](https://github.com/user-attachments/assets/0b0b5963-6809-4f03-b6c7-f5431c05b4cf)


## Architecture Components

### 1. **VPCs**
- **Test-VPC-01**
  - CIDR Block: `172.16.0.0/16`
  - Public Subnet
  - EC2 Instance with Internet Access
- **Test-VPC-02**
  - CIDR Block: `172.16.2.0/16`
  - Private Subnet
  - EC2 Instance with no direct Internet Access

### 2. **VPC Peering Connection**
- Established between `Test-VPC-01` and `Test-VPC-02`.
- Allows direct network routing between instances in both VPCs.
- Configured through AWS Management Console or AWS CLI.

### 3. **Internet Gateway**
- Attached to `Test-VPC-01` for external access.
- No Internet Gateway for `Test-VPC-02` (private communication only).

### 4. **Route Tables**
- **Test-VPC-01 Routing Table**
  - Routes to `172.16.2.0/16` via VPC Peering
  - Routes to `0.0.0.0/0` via Internet Gateway
- **Test-VPC-02 Routing Table**
  - Routes to `172.16.0.0/16` via VPC Peering

## Steps to Set Up VPC Peering
1. **Create Two VPCs**
   - Define subnets and associate them.
2. **Launch EC2 Instances**
   - One instance in each VPC.
3. **Create a VPC Peering Connection**
   - Request peering from `Test-VPC-01` to `Test-VPC-02`.
   - Accept the request in `Test-VPC-02`.
4. **Update Route Tables**
   - Add routes for peering connection in both VPCs.
5. **Modify Security Groups**
   - Allow inbound traffic from the peered VPC's CIDR block.
6. **Test Connectivity**
   - Use `ping` or other network tools to verify communication between EC2 instances.

## Verification
To test the setup, you can SSH into the EC2 instance in `Test-VPC-01` and try to reach the EC2 instance in `Test-VPC-02` using its private IP.
```sh
ping <private-ip-of-Test-VPC-02-instance>
```
If the setup is correct, the ping should be successful, confirming VPC Peering connectivity.

## Conclusion
This VPC Peering setup allows secure, private communication between two VPCs without traversing the public internet. It is useful for multi-tier applications, database connections, and cross-region deployments.<img width="723" alt="Screenshot 2025-03-28 at 11 26 50" src="https://github.com/user-attachments/assets/552d80fc-fcff-43a4-8f42-727ad8bdc7d7" />
<img width="710" alt="Screenshot 2025-03-28 at 11 26 43" src="https://github.com/user-attachments/assets/532dd63a-5a75-4270-8260-b175c0485657" />
<img width="1113" alt="Screenshot 2025-03-28 at 11 10 23" src="https://github.com/user-attachments/assets/0bc1b9fd-ddce-4a44-ab66-b8e0a7b6bb6c" />
<img width="1170" alt="Screenshot 2025-03-28 at 11 09 43" src="https://github.com/user-attachments/assets/c42d05af-7bcf-4c8d-8b55-c7163d7362a6" />
<img width="1191" alt="Screenshot 2025-03-28 at 10 53 58" src="https://github.com/user-attachments/assets/2190aa45-e625-4de1-8fb3-fa82c7552aa6" />
<img width="1199" alt="Screenshot 2025-03-28 at 10 47 59" src="https://github.com/user-attachments/assets/fb7a5d25-7e9c-4e96-aaed-e6c20375faeb" />
<img width="1187" alt="Screenshot 2025-03-28 at 10 46 22" src="https://github.com/user-attachments/assets/31ad6354-100a-467a-974c-4410a262d5fd" />


