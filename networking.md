# 📁 networking/

The `networking/` directory contains all infrastructure components related to **cloud networking architecture**. It defines how resources communicate with each other securely, reliably, and at scale. This layer is foundational for deploying highly available, fault-tolerant, and secure applications.

---

## 1. Virtual Private Cloud (VPC)

<p align="center">
  <img src="https://content.nordlayer.com/uploads/What_is_a_Virtual_Private_Cloud_scheme_15c7e05876.png"
       alt="VPC Architecture Diagram"
       width="45%"/>
  <img src="https://docs.aws.amazon.com/images/vpc/latest/userguide/images/how-it-works.png"
       alt="AWS VPC How It Works"
       width="45%"/>
</p>

A **Virtual Private Cloud (VPC)** is an isolated virtual network environment within a cloud provider. It allows full control over IP addressing, routing, and network security.

### Key Responsibilities

* Provides network isolation from other tenants
* Defines IP address ranges using CIDR blocks
* Acts as a parent container for subnets, gateways, and routing tables

### Common Configurations

* IPv4 and/or IPv6 CIDR allocation
* Internet Gateway attachment for public access
* NAT Gateway for outbound internet access from private networks
* Route tables to control traffic flow

### Benefits

* Strong network isolation
* Customizable network topology
* Enhanced security and compliance

---

## 2. Subnets

<p align="center">
  <img src="https://docs.aws.amazon.com/images/vpc/latest/userguide/images/vpc-example-private-subnets.png"
       alt="VPC with Public and Private Subnets"
       width="45%"/>
  <img src="https://cdn.prod.website-files.com/6340354625974824cde2e195/6578d079260c3223351bd0d3_6hBOTP_eTKiei4JgB1Ds52pEMmCFRCXP0n66tEh_gQBDNhQ8jtLcSWPPNxpEC3s6YjhsGqBj5bZ1ooFo07T1d16wGGoByH7C-QogSh1Ca2-aXt3QbXLYnrrOf0orVgZ3iwqZPizaUx3cUuAd1v9Uvq8.gif"
       alt="Private Subnet Traffic Flow Animation"
       width="45%"/>
</p>

**Subnets** divide a VPC into smaller, logical networks and are typically mapped to individual availability zones.

### Types of Subnets

* **Public Subnet**

  * Has a route to the Internet Gateway
  * Hosts resources like load balancers and bastion hosts
* **Private Subnet**

  * No direct internet access
  * Hosts application servers, databases, and internal services

### Key Characteristics

* Each subnet belongs to one availability zone
* Improves fault isolation and scalability
* Enables tier-based architecture (web, application, database)

---

## 3. Load Balancing

<p align="center">
  <img src="https://images.wondershare.com/edrawmax/templates/network-diagram-for-load-balancing.png"
       alt="Network Load Balancing Architecture Diagram"
       width="30%"/>
  <img src="https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AGb7hi5pqKmYYxEIUCJylHw.gif"
       alt="Load Balancer Traffic Distribution Animation"
       width="30%"/>
  <img src="https://assets.digitalocean.com/articles/high-availability/Diagram_1.png"
       alt="High Availability Architecture with Load Balancer"
       width="30%"/>
</p>


**Load Balancers** distribute incoming network traffic across multiple backend resources to ensure availability, scalability, and performance.

### Functions

* Traffic distribution across instances or containers
* Health checks to route traffic only to healthy targets
* SSL/TLS termination
* Session persistence (when required)

### Common Load Balancer Types

* **Application Load Balancer (Layer 7)**
  Routes traffic based on HTTP/HTTPS rules such as paths and headers.
* **Network Load Balancer (Layer 4)**
  Handles high-throughput, low-latency TCP/UDP traffic.

### Advantages

* Improves application availability
* Enables horizontal scaling
* Eliminates single points of failure

---

## 4. DNS (Domain Name System)

<p align="center">
  <img src="https://assets.bytebytego.com/diagrams/0175-dns-record-types-you-should-know.png"
       alt="DNS Record Types Overview"
       width="45%"/>
  <img src="https://storage.googleapis.com/gweb-cloudblog-publish/images/image2_YjKkxEG.max-2000x2000.jpg"
       alt="Cloud DNS Resolution Architecture"
       width="45%"/>
</p>

**DNS (Domain Name System)** translates human-readable domain names into IP addresses, enabling users and services to locate applications efficiently.

### Core Responsibilities

* Domain name resolution
* Traffic routing to load balancers or endpoints
* Health-based routing and failover

### Common DNS Record Types

* **A / AAAA** – Maps domain to IPv4/IPv6 address
* **CNAME** – Alias for another domain name
* **MX** – Mail server routing
* **TXT** – Verification and security records

### Advanced DNS Features

* Latency-based routing
* Geo-based routing
* Failover routing for disaster recovery

---

## 5. Security and Traffic Control (Cross-Cutting)

Although implemented in separate modules, networking integrates closely with:

* **Security Groups** – Stateful firewall rules at the resource level
* **Network ACLs** – Stateless traffic filtering at the subnet level
* **Routing Tables** – Control packet flow between subnets and gateways

These components ensure controlled, auditable, and secure network communication.

---

## 6. Repository Usage

The `networking/` directory typically includes:

* Infrastructure-as-Code (IaC) definitions (e.g., Terraform, CloudFormation)
* Modular and reusable networking components
* Environment-specific configurations (development, staging, production)

This structure enables **consistent, scalable, and repeatable** network deployments across environments.
