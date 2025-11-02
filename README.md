
# ** Challenge Lab: Creating a Static Website for the Café**


# ☕ Café Static Website on Amazon S3  
A challenge lab project demonstrating static website hosting, data protection, cost optimisation, and disaster recovery using **Amazon S3**.

This repository documents the architecture, configuration steps, and AWS services used to deploy a fully managed static website for a small café business. The implementation follows AWS architecture best practices across **availability**, **durability**, **security**, and **cost optimisation**.

---

## 📌 Project Overview

Frank and Martha run a small café and want to improve customer visibility. This project implements a simple, scalable, and low-cost static website hosted on Amazon S3. Beyond basic hosting, the lab explores enterprise-grade features such as:

- ✅ Static website hosting  
- ✅ Bucket policy for public access  
- ✅ S3 Versioning (accidental deletion protection)  
- ✅ Lifecycle rules (storage optimisation)  
- ✅ Cross-Region Replication (CRR)  
- ✅ Disaster Recovery planning  

---

## 🏗️ Architecture Diagram (Text Version)

```

Local Machine
│
▼
S3 Source Bucket (us-east-1)
├── Static Website Hosting Enabled
├── Versioning Enabled
├── Public Bucket Policy (Read-Only)
├── Lifecycle Rules:
│     ├── Transition old versions → S3 Standard-IA (30 days)
│     └── Delete old versions (365 days)
└── CRR → S3 Destination Bucket (Another Region)
├── Versioning Enabled
└── Receives replicated objects + delete markers

````

---

## ✅ Features Implemented

### **1. Static Website Hosting**
- Configured an S3 bucket (us-east-1) to host HTML/CSS/images.  
- Disabled “Block Public Access” and enabled ACLs.  
- Uploaded `index.html` and assets.  

### **2. Public Access Bucket Policy**
A read-only policy was applied to allow public viewing of all objects:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::cafe-static-website-demo-bucket/*"
    }
  ]
}
````

### **3. S3 Versioning**

* Enabled versioning to protect against accidental deletion or modification.
* Uploaded updated versions of the website to validate functionality.

### **4. Lifecycle Policies**

Two separate lifecycle rules were created:

#### Rule 1 – Storage Transition

Move previous versions to **S3 Standard-IA after 30 days**.

#### Rule 2 – Expiration

Delete previous versions **after 365 days**.

### **5. Cross-Region Replication (CRR)**

* Created a destination bucket in another AWS Region.
* Enabled versioning.
* Configured CRR in the source bucket.
* Used **CafeRole** IAM role for replication permissions.

---

## 📂 Repository Structure

```
├── index.html
├── images/
│   ├── *.jpg
│   └── *.png
├── css/
│   └── style.css
└── README.md
```

*( upload  actual files when pushing this lab to GitHub.)*

---

## ✅ Key Learning Outcomes

* Understand how to deploy static sites using S3.
* Apply IAM policies and bucket policies securely.
* Protect data using S3 Versioning.
* Optimise storage using lifecycle management.
* Implement cross-region redundancy for disaster recovery.
* Practice real-world cloud architectural patterns.

---

## 🚀 How to Deploy

1. Create an S3 bucket in **us-east-1**.
2. Disable "Block Public Access" and enable ACLs.
3. Upload your HTML/CSS/image files.
4. Enable static website hosting and choose `index.html`.
5. Apply the public read-only bucket policy.
6. Enable versioning.
7. Create lifecycle rules (Standard-IA + Expiration).
8. Create a second bucket in another Region.
9. Configure CRR from source → destination.

---

## 📘 References

* AWS S3 Documentation https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html#step4-add-bucket-policy-make-content-public
* AWS Well-Architected Framework https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
* Challenge Lab: *Creating a Static Website for the Café*

---

## 👩‍💻 Author

Created by an **ALX AWS Cloud Architect learner**, reflecting practical experience from hands-on AWS challenge labs and real-world cloud design patterns.

```
✅ A **more visually appealing diagram**?
```
