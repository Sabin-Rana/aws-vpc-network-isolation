# **AWS VPC Setup with Public and Private Subnets for aws-vpc-lab**

## **Project Overview**
This project demonstrates the creation of a Virtual Private Cloud (VPC) in AWS for **aws-vpc-lab**, focusing on the configuration of both public and private subnets for secure and isolated hosting of applications and services. The project also covers the setup of Internet Gateway (IGW) for public subnets, route tables configuration, and network security using NACLs and Security Groups.

## **Project Objectives**
- **Deploy VPC**: Set up a Virtual Private Cloud with public and private subnets.
- **Ensure Security**: Implement security controls using NACLs and Security Groups to restrict inbound and outbound traffic.
- **Enable Internet Access**: Configure Internet Gateway (IGW) for public subnet internet access.
- **Configure Routing**: Set up routing tables and subnet associations for proper traffic flow.

---

## **Implementation Steps**

### **Step 1: Planning and Design**

1. **VPC CIDR Block**: Chose `10.0.0.0/16` as the CIDR block for the VPC.
2. **Subnet Configuration**:
   - **Public Subnets**: `10.0.64.0/24`
   - **Private Subnets**: `10.0.200.0/24`
   - Checked for CIDR conflicts and corrected with `10.0.64.0/24` for the public subnet after encountering an error.

   **Screenshots**:
   - **Capture1**: Selected the **US East (Ohio)** region in the AWS Console to create the VPC.  
     ![Capture1](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture1.PNG)
   - **Capture2**: Navigated to the **VPC Dashboard** to begin creating the VPC.  
     ![Capture2](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture2.PNG)
   - **Capture3**: Created a new VPC with the CIDR block `10.0.0.0/16` and entered the required configurations.  
     ![Capture3](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture3.PNG)
   - **Capture4**: The VPC was successfully created with the specified CIDR block.  
     ![Capture4](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture4.PNG)

---

### **Step 2: Creating the VPC**

1. **VPC Creation**: Created a new VPC with the CIDR block `10.0.0.0/16`.
2. **Public and Private Subnets**: Created public and private subnets with CIDR blocks `10.0.64.0/24` and `10.0.200.0/24` respectively.

   **Screenshots**:
   - **Capture5**: Attempted to create a public subnet with the CIDR block `10.0.10.0/24` but received a CIDR conflict error.  
     ![Capture5](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture5.PNG)
   - **Capture6**: Error message indicating a **CIDR conflict** occurred because the new subnet's block overlaps with existing subnets.  
     ![Capture6](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture6.PNG)
   - **Capture7**: Used the **AWS CLI** to check for existing subnets and identify the conflict with the new subnet.  
     ![Capture7](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture7.PNG)
   - **Capture8**: After correcting the CIDR block, successfully created the **public subnet** with the `10.0.64.0/24` range.  
     ![Capture8](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture8.PNG)

---

### **Step 3: Configuring Internet Gateway (IGW)**

1. **Attach IGW to VPC**: AWS automatically attached an **Internet Gateway** (`aws-vpc-lab-igw`) to the VPC, enabling internet access for public subnets.
2. **No additional IGW required**: Since only one IGW per VPC is needed, no additional IGWs were created.

   **Screenshot**:
   - **Capture13**: **Internet Gateway (IGW)** automatically attached to the VPC, enabling internet access for public subnets.  
     ![Capture13](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture13.PNG)

---

### **Step 4: Configuring Route Tables**

1. **Create Route Table**: Created a route table named `RouteTable-Public-aws-vpc-lab` and added a route to `0.0.0.0/0` with the **Internet Gateway** as the target.
2. **Associate Route Table**: Associated the public subnets with the route table to enable internet access.

   **Screenshots**:
   - **Capture14**: Created a new route table `RouteTable-Public-aws-vpc-lab` and added a route pointing to `0.0.0.0/0` for internet traffic.  
     ![Capture14](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture14.PNG)
   - **Capture15**: Successfully created the route table with the new route to the Internet Gateway.  
     ![Capture15](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture15.PNG)
   - **Capture16**: Added the `0.0.0.0/0` route to ensure public subnets have access to the internet via the IGW.  
     ![Capture16](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture16.PNG)
   - **Capture17**: Route table successfully updated with the internet route and applied to the correct subnets.  
     ![Capture17](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture17.PNG)
   - **Capture18**: Edited subnet association to connect public subnets with the route table for internet access.  
     ![Capture18](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture18.PNG)
   - **Capture19**: Subnet association was successfully updated, and public subnets were associated with the route table.  
     ![Capture19](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture19.PNG)

---

### **Step 5: Network Access Control Lists (NACLs)**

1. **Create NACL**: Created a **Network Access Control List (NACL)** called `NACL-aws-vpc-lab` and associated it with the VPC.
2. **Edit Inbound Rules**: Configured inbound rules to manage traffic.

   **Screenshots**:
   - **Capture20**: Created the **NACL** for controlling traffic between public and private subnets.  
     ![Capture20](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture20.PNG)
   - **Capture21**: NACL creation was successful, and it was linked to the VPC.  
     ![Capture21](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture21.PNG)
   - **Capture22**: Edited inbound rules to control the types of traffic allowed into the VPC.  
     ![Capture22](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture22.PNG)

---

### **Step 6: Security Groups**

1. **Create Security Group**: Created a **Security Group** called `Securitygroup-aws-vpc-lab` to allow SSH and MySQL/Aurora access.
2. **Inbound Rules**: Configured inbound rules to allow SSH (port 22) from a specific IP, MySQL (port 3306), and HTTP (port 80) from anywhere.

   **Screenshots**:
   - **Capture23**: Created the **Security Group** for SSH and MySQL/Aurora access to the instances in the VPC.  
     ![Capture23](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture23.PNG)
   - **Capture24**: Edited inbound rules for SSH, MySQL, and HTTP access.  
     ![Capture24](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture24.PNG)
   - **Capture25**: Successfully created the security group with appropriate access rules.  
     ![Capture25](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture25.PNG)

---

### **Step 7: Security Best Practices**

1. **Private Subnet Security**: Ensured that the **private subnets** have restricted inbound traffic by associating appropriate NACLs and Security Groups.
2. **Traffic Control**: Denied unnecessary inbound traffic to ensure private subnets are isolated.

   **Screenshot**:
   - **Capture26**: NACL and Security Group successfully applied to the public subnet for enhanced security.  
     ![Capture26](https://github.com/Sabin-Rana/aws-vpc-network-isolation/blob/main/Screenshots/Capture26.PNG)

---

## **Security Best Practices**
- Implemented least privilege access using NACLs and Security Groups.
- Ensured private subnets are isolated and not directly accessible from the internet.
- Configured VPC to follow AWS security best practices for network access control.

---

## **Project Outcomes**
- Successfully created a VPC with public and private subnets.
- Configured internet access for public subnets with IGW and route tables.
- Established network security through NACLs and Security Groups.
- Ensured scalability and security for hosting applications in the VPC.

---

## **Screenshot Index**
- [Figure 1] - Region selection (Capture1.png)
- [Figure 2] - Accessing VPC Dashboard (Capture2.png)
- [Figure 3] - VPC creation details (Capture3.png)
- [Figure 4] - VPC creation success notification (Capture4.png)
- [Figure 5] - Subnet creation attempt (Capture5.png)
- [Figure 6] - CIDR conflict error (Capture6.png)
- [Figure 7] - CLI check for used subnets (Capture7.png)
- [Figure 8] - Public subnet creation success (Capture8.png)
- [Figure 9] - IGW attachment (Capture13.png)
- [Figure 10] - Route table creation (Capture14.png)
- [Figure 11] - Route table update success (Capture15.png)
- [Figure 12] - Adding route to route table (Capture16.png)
- [Figure 13] - Route table successfully updated (Capture17.png)
- [Figure 14] - Editing subnet association (Capture18.png)
- [Figure 15] - Subnet association success (Capture19.png)
- [Figure 16] - NACL creation (Capture20.png)
- [Figure 17] - NACL creation success (Capture21.png)
- [Figure 18] - Editing inbound rules (Capture22.png)
- [Figure 19] - Security group creation (Capture23.png)
- [Figure 20] - Inbound rules configuration (Capture24.png)
- [Figure 21] - Security group success (Capture25.png)
- [Figure 22] - NACL and Security Group application (Capture26.png)

---

## **Conclusion**
This project successfully demonstrates how to set up a secure and scalable AWS VPC with both public and private subnets, internet access, and effective network security. The implementation adheres to AWS best practices for cloud infrastructure and provides a robust environment for hosting applications securely.

---
