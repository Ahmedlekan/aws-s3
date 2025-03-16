# Amazon S3 Replication

Amazon S3 Replication is a robust feature designed to enhance data durability, availability, and compliance by automatically copying objects across S3 buckets.

### S3 Replication Configuration

1. Source:

- SSL: Ensures secure data transfer.

- Role: IAM role with necessary permissions.

- Same Account/Different Account: Replication can occur within the same AWS account or across different accounts.

2. Destination:

- Bucket Policy: Defines permissions for the destination bucket.

- Destination Bucket: The target bucket where objects are replicated.

### S3 Replication Options

1. Scope:

- All Objects or Subset: Choose to replicate all objects or a specific subset based on prefixes or tags.

2. Storage Class:

- Default: Maintains the original storage class.

- Custom: Option to change the storage class during replication.

3. Ownership:

- Default: Source account retains ownership.

- Change: Option to change ownership to the destination account.

4. Replication Time Control (RTC):
  
- Ensures that replication is completed within a predictable time frame.


### S3 Replication Considerations

1. Versioning:

- Required: Versioning must be enabled on both source and destination buckets.

- Not Retroactive: By default, replication is not retroactive for existing objects.

2. Batch Replication:

- Can be used to replicate existing objects.

3. Direction:

- One-Way: Source to destination.

- Bi-Directional: Both buckets replicate to each other.

4. Encryption:

- Supports unencrypted, SSE-S3, SSE-KMS (with extra configuration), and SSE-C.

5. Permissions:

- Source bucket owner needs permissions to objects.

6. Exclusions:

- System Events: Not replicated.

- Glacier/Deep Archive: Objects in these storage classes are not replicated.

7. Deletes:

- Default: Deletes are not replicated.

- Option: Can be enabled with DeleteMarkerReplication.


### Use Cases for S3 Replication

1. Same-Region Replication (SRR):

- Log Aggregation: Centralize logs from multiple buckets.

- PROD and TEST Sync: Keep production and test environments in sync.

- Resilience with Strict Sovereignty: Ensure data resilience within a specific region.

2. Cross-Region Replication (CRR):

- Global Resilience Improvements: Enhance data durability and availability across regions.

- Latency Reduction: Reduce latency by keeping data closer to end-users.



## Cross-Region Replication of an S3 Static Website 


### For the source bucket

1. Create a bucket

- Bucket Name

![Image](https://github.com/user-attachments/assets/4cebb7e7-1cdb-4bbf-a3b6-aaa3f1751f0a)

- AWS Region
E.g US East (N. Virginia) us-east-1

- Turn off block all public access

![Image](https://github.com/user-attachments/assets/2e7e12c3-503b-49f2-9139-931b5bd5b478)

- Enable Bucket Versioning

![Image](https://github.com/user-attachments/assets/9b73c8a8-ff49-4564-a203-f459ab47fcd2)

- Create Bucket

- Go to the perperties and enable Static website hosting

![Image](https://github.com/user-attachments/assets/64e0ada7-75d9-498b-b474-9c6a79359640)

- Go to the permission and edit the Bucket policy

- Replace the arn with your arn
```bash
{
    "Version":"2012-10-17",
    "Statement":[
      {
        "Sid":"PublicRead",
        "Effect":"Allow",
        "Principal": "*",
        "Action":["s3:GetObject"],
        "Resource":["arn:aws:s3:::examplebucket/*"]
      }
    ]
  }
```

### For the destination bucket

The process is the same, but this time, we will change the region to another region

- AWS Region
E.g US West (N. California) us-west-1

![Image](https://github.com/user-attachments/assets/4f91e4da-6aa2-45ff-b36b-59ea072381c4)


### Create Replication

- From the source bucket go to the management and create replication rules

![Image](https://github.com/user-attachments/assets/488d04ea-8f49-4dc8-9fb7-abc88d2cb557)

- Source Bucket

![Image](https://github.com/user-attachments/assets/556fe2c8-112c-48c8-8b38-006f317ea426)

- Destination

![Image](https://github.com/user-attachments/assets/16954670-fad1-488a-998c-d63408b835b1)

- Browse your s3 bucket and choose the destination bucket we created

![Image](https://github.com/user-attachments/assets/2abf59f9-573e-4736-8693-795f5722f70c)

- IAM Role
    - Click on create new IAM

- Click on save
    - Choose No, do not replicate existing objects since we do not have any object in the bucket now.  

- Go to the source bucket and upload your static website file

![Image](https://github.com/user-attachments/assets/14215513-d2b9-42ed-84cb-73f6fa5f25b5)

- Automatically, your static website file will be replicated into your destination bucket. 


## Conclusion

Amazon S3 Replication is a powerful feature for ensuring data durability, availability, and compliance. By understanding the configuration options, considerations, and use cases, you can effectively implement replication strategies to meet your specific needs. Whether for log aggregation, environment synchronization, or global resilience, S3 Replication offers flexible and robust solutions for data management.
