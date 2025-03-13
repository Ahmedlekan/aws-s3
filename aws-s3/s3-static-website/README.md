# Hosting a Static Website on Amazon S3

Amazon S3 provides a simple and cost-effective way to host static websites. This guide will walk you through the process of setting up a static website using S3, configuring public access, and linking it to a custom domain via Route 53.

## Steps to Host a Static Website on S3

1. Create an S3 Bucket

![Image](https://github.com/user-attachments/assets/519786eb-8149-4e3f-80e6-fb06478f582c)

Bucket Name:

- The bucket name must exactly match your registered domain name in Route 53 (e.g., www.example.com or example.com).

Bucket names must be globally unique and follow S3 naming rules:

- 3–63 characters.

- Lowercase letters, numbers, and hyphens only.

- Cannot be an IP address.

1.2. Disable Block Public Access:

![Image](https://github.com/user-attachments/assets/0b7fbeea-85e8-4e77-9d76-376c82bddf24)

Since this is a public website, you need to disable Block Public Access:

- Uncheck Block all public access and confirm.


2. Enable Static Website Hosting

![Image](https://github.com/user-attachments/assets/6c103c62-77dd-49c5-9943-20379b33db12)

Go to the Properties tab of your bucket.

Scroll down to Static website hosting and click Edit.

Enable Static website hosting.

Set the following:

![Image](https://github.com/user-attachments/assets/7498c36c-9f6f-4f64-bfbc-458f51e9486b)

- Index document: index.html (this is the default homepage).

- Error document: error.html (this is displayed when a page is not found).

Save the changes.

Copy the Website endpoint URL. This is the URL you’ll use to access your website.


3. Upload Website Files

![Image](https://github.com/user-attachments/assets/14215513-d2b9-42ed-84cb-73f6fa5f25b5)

Go to the Objects tab in your bucket.

Click Upload or drag and drop your website files (e.g., index.html, error.html, CSS, JS, and images).

Ensure the files are publicly accessible:

- Use a bucket policy to grant public access.


4. Set Bucket Policy for Public Access

To allow public access to your website, add the following bucket policy. Replace examplebucket with your bucket name.

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::examplebucket/*"
    }
  ]
}
```

Principal: "*" allows public access.

Action: "s3:GetObject" allows users to read objects.

Resource: Specifies the bucket and objects (/* means all objects in the bucket).


5. Test Your Website

Paste the Website endpoint URL into your browser.

Verify that your website loads correctly.









   
