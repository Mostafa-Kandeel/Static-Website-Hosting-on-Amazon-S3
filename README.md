# Static Website Hosting on Amazon S3

This guide provides step-by-step instructions to host a static website on Amazon S3.

## Prerequisites
- AWS account with access to the S3 service.
- Basic knowledge of uploading files and managing permissions.
- Static website files (e.g., `index.html`, CSS, JavaScript).

## Steps

### 1. Create an S3 Bucket
- Log in to the AWS Management Console.
- Navigate to S3 and click "Create bucket."
- Enter a unique bucket name (e.g., `my-static-website-2025`).
- Select a region and uncheck "Block all public access" (to be configured later).
- Click "Create bucket."

### 2. Enable Static Website Hosting
- Open the bucket in the S3 console.
- Go to the "Properties" tab.
- Scroll to "Static website hosting" and click "Edit."
- Enable it, set `index.html` as the index document, and optionally set an error document (e.g., `error.html`).
- Save changes and note the endpoint URL (e.g., `http://my-static-website-gym-2025.s3-website-us-east-1.amazonaws.com`).

### 3. Upload Website Files
- Go to the "Objects" tab in the bucket.
- Upload your static files (e.g., `index.html`, `style.css`).
- Ensure `index.html` is at the root level.

### 4. Set Bucket Policy
- Go to the "Permissions" tab.
- Edit the bucket policy with the following JSON:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "PublicReadGetObject",
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::my-static-website-2025/*"
      }
    ]
  }
  ```
- Replace `my-static-website-2025` with your bucket name.
- Save the policy.

### 5. Test the Website
- Open the static website endpoint URL in a browser.
- Verify the `index.html` page loads correctly.

### 6. Optional: Configure Custom Domain
- Set up a CNAME record in your DNS provider (e.g., Route 53) pointing to the S3 endpoint.
- Ensure the bucket name matches the domain (e.g., `www.example.com`).

### 7. Optional: Enable HTTPS
- Use Amazon CloudFront to add HTTPS.
- Create a distribution, set the S3 bucket as the origin, and configure an SSL certificate via AWS Certificate Manager (ACM).

## Notes
- S3 static websites support HTTP by default; HTTPS requires CloudFront.
- Ensure "Block Public Access" is adjusted to allow public read access.
- For dynamic content, consider integrating with AWS Lambda.




## Troubleshooting
- If the site doesn’t lck the bucket policy and public access settings.
- Verify the index document name matches the uploaded file.
