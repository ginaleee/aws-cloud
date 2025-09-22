# AWS Storage & Database

This section covers the differences between relational and NoSQL databases in AWS, how to analyze application data requirements, and how to justify database choices in real-world scenarios.

---

## Relational Database (Amazon RDS)

- **Schema**: Fixed, predefined schema (tables, rows, columns).
- **Scalability**: Primarily vertical scaling (add CPU/RAM).
- **Data Structure**: SQL queries, supports complex joins and transactions.
- **Use Cases**: Financial systems, e-commerce, applications requiring strict data consistency and analytics.

---

## NoSQL Database (Amazon DynamoDB)

- **Schema**: Flexible, schema-less design (e.g., JSON attributes).
- **Scalability**: Horizontal scaling (millions of requests/sec).
- **Data Structure**: Key-value/document store, optimized for predictable access patterns.
- **Use Cases**: Real-time bidding, gaming, user profiles, mobile apps.

---

## Choosing Between RDS and DynamoDB

### Key Questions to Ask:
1. **Data Structure & Relationships**  
   - Complex queries, joins → RDS  
   - Dynamic or semi-structured data → DynamoDB  

2. **Scalability & Performance**  
   - Predictable workloads, moderate scale → RDS  
   - Rapid growth, massive scale, low latency → DynamoDB  

3. **Consistency & Integrity**  
   - Strong ACID guarantees → RDS  
   - Eventual consistency acceptable → DynamoDB  

4. **Security & Compliance**  
   - Both offer encryption, IAM, auditing; consider regulatory needs (e.g., PCI, HIPAA).

---

## Case Study: Social Media User Profiles

- **Why DynamoDB?**
  - Horizontal scalability for millions of users.
  - Flexible schema for evolving profile fields.
  - Cost-effective with on-demand capacity.
  - Works seamlessly with serverless (AWS Lambda) + unstructured storage (Amazon S3).

---

## Integration with Other AWS Services

- **Compute**
  - Best with AWS Lambda (serverless event-driven architecture).
  - EC2 possible but less aligned with DynamoDB’s scaling model.

- **Storage**
  - DynamoDB stores structured metadata.
  - Amazon S3 stores unstructured data (images, videos, files).

---

✅ **Summary**:  
- Use **RDS** for structured, transaction-heavy workloads.  
- Use **DynamoDB** for flexible, large-scale, low-latency workloads.  
- Many modern architectures combine both (polyglot persistence).  
