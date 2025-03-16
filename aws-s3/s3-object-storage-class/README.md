# S3 Oject Storage Class

![Image](https://github.com/user-attachments/assets/337ef4bb-9214-4c29-8a90-8be63f530e85)

### Amazon S3 (Simple Storage Service) Standard storage class features and pricing. Here are the key points:

1. HTTP/1.1 200 OK Response: When objects are stored, the S3 API Endpoint provides this response.

2. Latency and Availability: S3 Standard offers low latency (milliseconds for the first byte) and objects can be made publicly available.

3. Pricing:

- Storage: Billed on a per GB per month basis.

- Data Transfer: Free for data transfer IN, but there is a charge per GB for data transfer OUT.

- Requests: Charged per 1,000 requests.

- No Retrieval Fee: There is no specific retrieval fee.

- No Minimums: No minimum duration or size requirements.

4. Durability and Availability:

- Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

- Replication: Objects are replicated across at least three Availability Zones (AZs) within an AWS region.

- Data Integrity: Uses Content-MDS Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption.

5. Use Case: S3 Standard is recommended for frequently accessed data that is important and non-replaceable.

This information is useful for understanding the reliability, performance, and cost structure of using Amazon S3 Standard for storing and managing data in the cloud.



### Amazon S3 Standard-IA (Infrequent Access) storage class features and pricing. Here are the key points:

1. Data Retrieval Fee: S3 Standard-IA incurs a per GB data retrieval fee, making the overall cost higher for frequently accessed data.

2. Minimum Duration Charge: There is a minimum duration charge of 30 days. Even if objects are stored for less than 30 days, the minimum billing period still applies.

3. Minimum Capacity Charge: There is a minimum capacity charge of 128KB per object. Objects smaller than 128KB will still be billed as if they were 128KB.

4. Durability and Availability:

- Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

- Replication: Objects are replicated across at least three Availability Zones (AZs) within an AWS region.

- Data Integrity: Uses Content-MDS Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption.

5. Use Case: S3 Standard-IA is recommended for long-lived data that is important but accessed infrequently.

This information is useful for understanding the cost structure and appropriate use cases for Amazon S3 Standard-IA, particularly for data that is not frequently accessed but still requires high durability and availability.



### Amazon S3 One Zone-IA (Infrequent Access) storage class features and pricing. Here are the key points:

1. Data Retrieval Fee: S3 One Zone-IA incurs a per GB data retrieval fee, making the overall cost higher for frequently accessed data.

2. Single Availability Zone (AZ): Unlike Standard or Standard-IA, One Zone-IA does not replicate data across multiple AZs. Instead, it stores data in a single AZ within the region, which reduces resilience.

3. Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

4. Minimum Duration Charge: There is a minimum duration charge of 30 days. Even if objects are stored for less than 30 days, the minimum billing period still applies.

5. Minimum Capacity Charge: There is a minimum capacity charge of 128KB per object. Objects smaller than 128KB will still be billed as if they were 128KB.

6. Use Case: S3 One Zone-IA is recommended for long-lived data that is non-critical and replaceable, and where access is infrequent. It is suitable for data that can be recreated or is less critical in case of an AZ failure.

This information is useful for understanding the cost structure and appropriate use cases for Amazon S3 One Zone-IA, particularly for data that is not frequently accessed and can afford the reduced resilience of being stored in a single AZ.




### Amazon S3 Glacier Instant Retrieval storage class features and pricing. Here are the key points:

1. Cost Structure: Similar to S3 Standard-IA, Glacier Instant offers cheaper storage but more expensive retrieval costs, making it less economical for frequently accessed data.

2. Data Retrieval Fee: Glacier Instant incurs a per GB data retrieval fee, which increases the overall cost if data is accessed frequently.

3. Minimum Duration Charge: There is a minimum duration charge of 90 days. Even if objects are stored for less than 90 days, the minimum billing period still applies.

4. Minimum Capacity Charge: There is a minimum capacity charge of 128KB per object. Objects smaller than 128KB will still be billed as if they were 128KB.

5. Durability and Availability:

- Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

- Replication: Objects are replicated across at least three Availability Zones (AZs) within an AWS region.

- Data Integrity: Uses Content-MDS Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption.

6. Use Case: S3 Glacier Instant is recommended for long-lived data that is accessed infrequently, typically once per quarter, but requires millisecond access when needed.

This information is useful for understanding the cost structure and appropriate use cases for Amazon S3 Glacier Instant Retrieval, particularly for data that is rarely accessed but needs to be available quickly when required.



### Amazon S3 Glacier Flexible Retrieval storage class features and pricing. Here are the key points:

1. Access Restrictions: Objects stored in Glacier Flexible cannot be made publicly accessible. Accessing the data (beyond object metadata) requires a retrieval process.

2. Minimum Size and Duration:

- Minimum Size: 40KB per object.

- Minimum Duration: 90 days. Even if objects are stored for less than 90 days, the minimum billing period still applies.

3. Durability and Availability:

- Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

- Replication: Objects are replicated across at least three Availability Zones (AZs) within an AWS region.

- Data Integrity: Uses Content-MDS Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption.

4. Use Case: S3 Glacier Flexible is recommended for archival data where frequent or real-time access is not needed (e.g., accessed yearly). Retrieval times range from minutes to hours.

5. Retrieval Process:

- Temporary Storage: Retrieved data is temporarily stored in S3 Standard-IA.

- Retrieval Options:

    - Expedited: 1-5 minutes.
    
    - Standard: 3-5 hours.
    
    - Bulk: 5-12 hours.

- Cost: Faster retrieval options are more expensive.

6. First Byte Latency: The time to access the first byte of data ranges from minutes to hours.

This information is useful for understanding the cost structure and appropriate use cases for Amazon S3 Glacier Flexible Retrieval, particularly for long-term archival data that is rarely accessed and does not require immediate availability.



### Amazon S3 Glacier Deep Archive storage class features and pricing. Here are the key points:

1. Access Restrictions: Objects stored in Glacier Deep Archive cannot be made publicly accessible. Accessing the data (beyond object metadata) requires a retrieval process.

2. Minimum Size and Duration:

- Minimum Size: 40KB per object.

- Minimum Duration: 180 days. Even if objects are stored for less than 180 days, the minimum billing period still applies.

3. Durability and Availability:

- Durability: 99.999999999% (11 nines) durability, meaning 1 object loss per 10,000 years for 10,000,000 objects.

- Replication: Objects are replicated across at least three Availability Zones (AZs) within an AWS region.

- Data Integrity: Uses Content-MDS Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption.

4. Use Case: S3 Glacier Deep Archive is recommended for archival data that rarely, if ever, needs to be accessed. Examples include legal or regulatory data storage. Retrieval times can range from hours to days.

5. Retrieval Process:

- Temporary Storage: Retrieved data is temporarily stored in S3 Standard-IA.

- Retrieval Options:

    - Standard: 12 hours.
    
    - Bulk: Up to 48 hours.

- First Byte Latency: The time to access the first byte of data ranges from hours to days.

6. Comparison to Glacier: Glacier Deep Archive has much longer retrieval times compared to other Glacier storage classes.

This information is useful for understanding the cost structure and appropriate use cases for Amazon S3 Glacier Deep Archive, particularly for long-term archival data that is almost never accessed and does not require immediate availability.



### S3 Intelligent-Tiering

Amazon S3 Intelligent-Tiering is designed to optimize storage costs by automatically moving objects between different access tiers based on their usage patterns. This storage class is ideal for long-lived data with changing or unpredictable access patterns.

Key Features:

1. Automatic Tiering:

- Monitoring & Automated Migration: Intelligent-Tiering continuously monitors access patterns and automatically moves objects that haven’t been accessed for 30 days to a low-cost infrequent access tier. Objects can further be moved to archive instant access, archive access, or deep archive tiers based on continued inactivity.

- Frequent Access Tier: Objects that are accessed regularly remain in the frequent access tier.

- No Retrieval Fees: There are no retrieval fees for accessing objects, making it cost-effective for data with unpredictable access patterns.

2. Tier Options:

- Frequent Access: For regularly accessed data.

- Infrequent Access: For data accessed less frequently.

- Archive Instant Access: For data that requires millisecond access but is rarely accessed.

- Archive Access: For data that is accessed very infrequently, with retrieval times of minutes to hours.

- Deep Archive: For data that is almost never accessed, with retrieval times of hours to days.

3. Configuration:

- Bucket-Level Configuration: Intelligent-tiering archive configurations can be set at the bucket level, using prefixes and tags.

- Customizable Tier Transitions: You can configure the system to move objects to even "colder" tiers when they aren’t accessed for specific periods (e.g., 90, 180, or 730 days).

4. Cost Structure:

- Monitoring & Automation Cost: There is a monitoring and automation cost per 1,000 objects.

- Tier Costs: The frequent access tier costs the same as S3 Standard, the infrequent access tier costs the same as Standard-IA, and the archive tiers are comparable to their S3 Glacier equivalents.


Use Cases:

- Long-Lived Data with Changing Access Patterns: Ideal for data that is stored for long periods but has unpredictable access patterns.

- Cost Optimization: Suitable for organizations looking to optimize storage costs without manual intervention.

- Regulatory and Compliance Data: Useful for data that needs to be retained for compliance but is rarely accessed.

Benefits:

- Cost Efficiency: Automatically optimizes storage costs by moving data to the most cost-effective tier based on access patterns.

- Ease of Use: No need for manual intervention or complex management policies.

- Flexibility: Customizable tier transitions to meet specific data lifecycle needs.




