Here’s a **summarized note** for your Reading 4.4 on **Amazon Elastic Load Balancing (ELB):**

---

# **AWS Elastic Load Balancing (ELB) – Summary**

### **What is Load Balancing?**

* Distributes traffic across multiple resources (e.g., EC2 instances).
* Improves **availability, scalability, and fault tolerance**.
* **Round-robin** is common: sends requests sequentially across servers.
* AWS provides **Elastic Load Balancing (ELB)** so you don’t need to manage software load balancers yourself.

---

### **Key Features of ELB**

* Managed, highly available, auto-scaling.
* Supports EC2, containers, Lambda, IP addresses (including on-premises).
* Must deploy across **multiple AZs** for HA.

---

### **Health Checks**

* Validates that backend targets are working.
* Should check dependencies (DB, S3, etc.) not just open ports.
* Example: `/monitor` page for deeper app checks.
* **Integration with EC2 Auto Scaling:**

  * If unhealthy → ELB stops routing + Auto Scaling replaces instance.
  * During scale-in, ELB uses **connection draining** (deregistration delay) to let active sessions finish before shutdown.

---

### **ELB Components**

* **Listeners** → define client-side connection (protocol + port).
* **Target Groups** → backend destinations (EC2, Lambda, IPs). Each has health checks.
* **Rules** → conditions for routing traffic from listener → target group.

---

### **Application Load Balancer (ALB)**

* **Protocols:** HTTP/HTTPS (Layer 7).
* **Advanced Routing:** by path (`/upload`), host, headers, method, source IP.
* **Responses:** fixed responses, redirects (e.g., HTTP → HTTPS).
* **TLS offloading:** offloads SSL/TLS; integrates with IAM & AWS Certificate Manager (ACM).
* **Authentication:** supports OpenID Connect, SAML, LDAP, Microsoft AD.
* **Security:** use security groups to restrict traffic.
* **Algorithms:**

  * *Round-robin* (default).
  * *Least outstanding requests* (balances uneven workloads).
* **Sticky sessions:** via HTTP cookies.
* **Best for:** web apps needing Layer 7 routing, user authentication, or redirects.

---

### **Network Load Balancer (NLB)**

* **Protocols:** TCP, UDP, TLS (Layer 4).
* **Algorithm:** flow hash (based on protocol, IP, ports, sequence number).
* **Sticky sessions:** based on client IP.
* **TLS offloading:** supported.
* **Performance:** millions of requests/sec, instant scaling.
* **IP handling:** supports **static/elastic IPs**, preserves **client source IP**.
* **Best for:** ultra-high performance, low latency, or when client source IP/static IPs are required.

---

### **Choosing ALB vs. NLB**

| Feature                                       | ALB         | NLB           |
| --------------------------------------------- | ----------- | ------------- |
| Protocols                                     | HTTP, HTTPS | TCP, UDP, TLS |
| Advanced routing (host, path, headers, query) | ✔           | ✘             |
| User authentication                           | ✔           | ✘             |
| Redirects & fixed responses                   | ✔           | ✘             |
| Connection draining                           | ✔           | ✔             |
| IP addresses as targets                       | ✔           | ✔             |
| Static/Elastic IP                             | ✘           | ✔             |
| Preserve client source IP                     | ✘           | ✔             |

---

✅ **Quick Takeaway:**

* Use **ALB** for **web applications (Layer 7 features)** like routing, redirects, auth.
* Use **NLB** for **high-performance, low-level traffic (Layer 4)** or when IP-level control is needed.

---


