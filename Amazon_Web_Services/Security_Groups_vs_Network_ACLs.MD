# Difference Between Security Groups vs Network ACLs (Access Control Lists)

In AWS, **Security Groups** and **Network ACLs (Access Control Lists)** are both used to control network traffic, but they operate at different levels and have distinct functionalities.  

### **Security Groups (SGs)**
- **Instance-Level Protection** – Security Groups act as virtual firewalls controlling inbound and outbound traffic at the **instance level**.
- **Stateful** – They remember the connection state; if an inbound rule allows traffic, the response is automatically allowed outbound.
- **Rules Apply Per Instance** – Each EC2 instance can have multiple security groups, and all rules are evaluated together.
- **Allows Traffic by Default** – You specify which traffic is permitted; anything not explicitly allowed is blocked.
- **Supports Only Allow Rules** – You can **allow** specific traffic but **cannot** explicitly deny connections.

### **Network ACLs (NACLs)**
- **Subnet-Level Protection** – Network ACLs operate at the **subnet level**, controlling traffic entering or leaving.
- **Stateless** – They do **not** track connection state, meaning both inbound and outbound rules must be explicitly defined.
- **Rules Apply Per Subnet** – Affect all instances within the associated subnet.
- **Deny Rules Are Allowed** – You can **explicitly allow or deny** traffic, making them useful for blocking specific IPs or ports.
- **Default Rule Denies All** – If no matching rule is found, the request is denied.

### **Key Differences**
| Feature              | Security Groups | Network ACLs |
|----------------------|----------------|--------------|
| **Scope**            | Instance level  | Subnet level |
| **Stateful/Stateless** | Stateful       | Stateless    |
| **Allows/Deny Rules** | Only Allow     | Allow & Deny |
| **Default Behavior**  | Denies all unless explicitly allowed | Denies all if no rule exists |
| **Evaluation Order** | All rules checked | Rules evaluated in order |

### **When to Use Which?**
- Use **Security Groups** for controlling **instance-specific access**.
- Use **Network ACLs** for broader **subnet-wide filtering** (e.g., blocking specific IP ranges).
- Combine both for **layered security**.

### Reference:
1. [AWS documentation on VPC](https://docs.aws.amazon.com/vpc/latest/userguide/security-groups.html)
2. [AWS documentation on VPC Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
3. [AWS documentation on VPC ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)


