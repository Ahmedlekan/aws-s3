# S3 Object Encryption: SSE-S3 vs. SSE-KMS

Amazon S3 provides multiple options for Server-Side Encryption (SSE) to secure your data at rest. Two common methods are SSE-S3 (encryption managed by S3) and SSE-KMS (encryption managed by AWS Key Management Service).

## 1. SSE-S3: Encryption Managed by S3

### Steps to Use SSE-S3

Create an S3 Bucket:

![Image](https://github.com/user-attachments/assets/6198e8fe-6a36-4673-b8f2-c7fcb4beca2c)

- Go to the S3 console and create a new bucket.

Upload an Object:

- Upload an object (e.g., sse-s3-dweez.jpg) to the bucket.

Enable Server-Side Encryption:

![Image](https://github.com/user-attachments/assets/d8415a34-e36d-48c0-a687-d06b137ef6f7)

- During the upload, enable Server-Side Encryption and choose SSE-S3.

- S3 automatically manages the encryption keys for you.


### Key Characteristics of SSE-S3

- Encryption Keys: Managed by S3.

- Access Control: No customer control over encryption keys.

- Use Case: Suitable for scenarios where you do not need granular control over encryption keys.


## 2. SSE-KMS: Encryption Managed by KMS

### Steps to Use SSE-KMS

- Use the same bucket for both the sse-s3 and sse-kms.

Create a KMS Key:

![Image](https://github.com/user-attachments/assets/1f1250a1-2021-4464-a054-6f5475d8cfbf)

- Go to the KMS console and create a new key.

- Do not enable Key Administrators or Key Users during key creation.

Upload an Object:

- Upload an object (e.g., sse-kms-ginny.jpg) to the bucket.

Enable Server-Side Encryption:

![Image](https://github.com/user-attachments/assets/daa88c75-c464-4bde-b152-6ffb9c41ffdd)

- During the upload, enable Server-Side Encryption and choose SSE-KMS.

- Select the KMS key you created.

### Key Characteristics of SSE-KMS

- Encryption Keys: Managed by KMS.

- Access Control: Granular control over who can use the key for encryption/decryption.

- Use Case: Suitable for scenarios requiring strict access control and auditability.


## Role Separation with SSE-KMS

### Scenario

- As an IAM admin, you have full access to the AWS account, including S3 and KMS.

- You want to enforce role separation so that IAM users cannot decrypt objects encrypted with SSE-KMS, even if they have access to the S3 bucket.

### Steps to Implement Role Separation

1. Create a Deny Policy for KMS:

- Create an inline policy named denyKMS for your IAM user/role.

- The policy denies all KMS actions.

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```
2. Test Access:

Try to open the objects:

![Image](https://github.com/user-attachments/assets/4d1a53d0-83a6-454a-b9e0-2dc4d3987ee4)

- SSE-S3 Object (sse-s3-dweez.jpg): Opens successfully because encryption keys are managed by S3.

- SSE-KMS Object (sse-kms-ginny.jpg): Access is denied because the IAM user cannot decrypt the object without KMS permissions. 

3. Delete the SSE-KMS Object:

- You can still delete the object (sse-kms-ginny.jpg) because you have full access to S3.

- However, you cannot open or decrypt the object due to the denyKMS policy.


## Conclusion

SSE-S3 is a simple encryption method managed by S3, suitable for basic use cases.

SSE-KMS provides advanced encryption key management and access control, ideal for sensitive data and compliance requirements.

By implementing a deny policy for KMS, you can enforce role separation, ensuring that only authorized users can decrypt objects encrypted with SSE-KMS.

This approach allows you to maintain control over your encryption keys while ensuring that unauthorized users cannot access sensitive data, even if they have access to the S3 bucket.



