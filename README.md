### **TagFinder CloudFormation Template**

#### **Overview**
This repository contains an **AWS CloudFormation template** that provisions the entire infrastructure required to run the  [**TagFinder web application**](https://github.com/Listowel-Moro/tag-finder)
The repository is integrated with **AWS GitSync**, ensuring that any updates to the template automatically trigger the **CloudFormation stack update**.

---

### **Features**
a. **Custom VPC with Public & Private Subnets** – Secure application architecture  
b. **ECS Fargate Cluster** – Serverless container orchestration  
c. **Application Load Balancer (ALB)** – Distributes incoming traffic  
d. **Amazon S3 Bucket** – Stores images  
e. **IAM Roles & Security Groups** – Granular access control  
f. **CodeDeploy with Blue/Green Deployment** – Zero-downtime deployments  
g. **Auto Scaling** – Handles traffic spikes  
h. **GitSync Integration** – Auto-provisions resources when the template is updated

---

### **CloudFormation Deployment Workflow**
1. **CloudFormation Stack is Created**
2. **GitSync Monitors Repo** for changes
3. **Upon Update, CloudFormation Auto-Provisions Resources**
4. **Application Deploys via ECS Fargate & ALB**

---

### **CloudFormation Template Breakdown**
#### **1️⃣ VPC & Networking**
- A **custom VPC** spanning multiple **Availability Zones**
- **Public & Private Subnets** for different resources
- **Internet Gateway + NAT Gateway** for secure internet access

#### **2️⃣ ECS & Load Balancer**
- **ECS Fargate Cluster** for running containerized workloads
- **Application Load Balancer (ALB)** for routing traffic
- **Target Groups & Listeners** for **Blue/Green Deployment**

#### **3️⃣ IAM Roles & Security**
- **IAM Roles for ECS, S3, CodePipeline, and CodeDeploy**
- **Security Groups for ALB & ECS** (restricting direct internet access)

#### **4️⃣ CI/CD with GitSync & CodeDeploy**
- CloudFormation is **automatically updated via GitSync**
- **CodePipeline & CodeDeploy** handle deployments when a new Docker image is pushed

---

### **Deployment Instructions**
#### **Option 1: Deploy via AWS CLI**
Run the following command to deploy the CloudFormation stack:
```bash
aws cloudformation create-stack --stack-name TagFinderStack --template-body file://cloudformation-template.yml --capabilities CAPABILITY_NAMED_IAM
```

#### **Option 2: Deploy via AWS Console**
1. Navigate to **AWS CloudFormation Console**
2. Click **Create Stack** → **Upload a template file**
3. Select **cloudformation-template.yml** and click **Next**

---

### **GitSync Integration**
To enable **automatic updates** via GitSync:
1. Connect your GitHub repository to **AWS CloudFormation**
2. Enable **"GitSync"** in the CloudFormation settings
3. Any updates to `cloudformation-template.yml` will automatically provision resources
