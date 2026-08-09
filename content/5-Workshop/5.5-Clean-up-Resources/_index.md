---
title: "Clean-up"
date: 2026-08-07
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---



> Cleaning up AWS resources after completing the practical activities is necessary to avoid unexpected charges on the AWS account.

## Objective

After completing the deployment and testing of the **AI Learning Assistant Platform**, clean up AWS resources that are no longer in use.

This helps release resources, reduce unnecessary costs, and ensure that the AWS account does not maintain services that are no longer required.

---

## Implementation

### 1. Terminate the Amazon EC2 Instance

After completing the testing process, terminate the EC2 Instance used to deploy the system.

Steps:

1. Access the **Amazon EC2 Console**.
2. Select **Instances**.
3. Select the **ai-learning-assistant** Instance.
4. Select **Instance state**.
5. Select **Terminate instance**.
6. Confirm the termination operation.

After the operation is completed, check the Instance status. The Instance will change to **Shutting-down** and then to **Terminated**.

> **Figure 5.5.1. Terminating the Amazon EC2 Instance after completing the deployment.**

> ![Figure 5.5.1](/images/5.5.1.png)

---

### 2. Release the Elastic IP

An Elastic IP that is no longer in use should be released to avoid unnecessary charges when the IP address is not associated with a required resource.

Steps:

1. Access the **Amazon EC2 Console**.
2. Select **Elastic IPs**.
3. Select the Elastic IP that was used by the EC2 Instance.
4. Select **Actions**.
5. If the IP is still associated with the Instance, select **Disassociate Elastic IP address** first.
6. Select **Actions → Release Elastic IP address**.
7. Confirm the release operation.

After the operation is completed, the Elastic IP will be released and will no longer be allocated to the AWS account.

> **Figure 5.5.2. Releasing the Elastic IP address after completing the deployment.**

> ![Figure 5.5.2](/images/5.5.2.png)

---

### 3. Delete the Amazon ECR Repository

If the Amazon ECR Repository is no longer required, delete the Repository and its associated Docker Images.

Steps:

1. Access **Amazon Elastic Container Registry (Amazon ECR)**.
2. Select **Repositories**.
3. Select the **ai-learning-assistant** Repository.
4. Select **Delete**.
5. Confirm the deletion of the Repository.

> **Note:** Deleting the Repository will also delete the Docker Images stored inside it. Only perform this operation when the Images are no longer required.

> **Figure 5.5.3. Deleting the Amazon ECR Repository of the AI Learning Assistant Platform.**

> ![Figure 5.5.3](/images/5.5.3.png)

---

### 4. Delete Data from Amazon S3

If the system uses **Amazon S3** to store backup data or temporary data, empty the Bucket before deleting it.

Steps:

1. Access **Amazon S3**.
2. Select the Bucket containing the system backup data.
3. Select **Empty**.
4. Confirm the deletion of all data in the Bucket.
5. After the Bucket has been emptied, select **Delete**.
6. Enter the Bucket name to confirm the deletion.

> **Note:** Carefully review the data stored in the Bucket before deleting it to avoid losing required data.

> **Figure 5.5.4. Deleting the Amazon S3 Bucket after completing the deployment.**

> ![Figure 5.5.4](/images/5.5.4.png)

---

## Verification After Clean-up

After completing the clean-up steps, check the AWS services to ensure that unused resources have been deleted or released.

The following resources can be checked:

- **Amazon EC2:** The Instance has changed to the **Terminated** state.
- **Elastic IP:** The IP address is no longer allocated.
- **Amazon ECR:** The **ai-learning-assistant** Repository has been deleted if it is no longer in use.
- **Amazon S3:** The Bucket no longer contains data or has been deleted if it is no longer required.

---

## Result

After completing the **Clean-up** process, AWS resources that are no longer required by the **AI Learning Assistant Platform** have been deleted or released.

Resource clean-up helps to:

- Reduce unexpected AWS costs.
- Release resources that are no longer in use.
- Ensure that AWS resources are managed efficiently.
- Complete the deployment, testing, and operation lifecycle of the project.

> **Note:** If the project still needs to use EC2, ECR, or S3 for development or demonstration purposes, the corresponding resources do not need to be deleted. Only perform the Clean-up process for resources that are no longer required.

Mình cũng sửa nhẹ lỗi chính tả trong bản gốc của bạn: