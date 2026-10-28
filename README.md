# Responsive Portfolio — AWS S3 Assignment

A responsive, single-page portfolio built with HTML, CSS, and vanilla JavaScript.

## Included requirements
- Hero, About, Projects, Contact, and footer sections
- Hero call-to-action buttons
- Three project cards
- Google Fonts: DM Sans and Space Grotesk
- Font Awesome icon set
- Responsive mobile navigation and layouts
- Semantic HTML, accessible labels, and reduced-motion support

## Preview locally
1. Extract the ZIP.
2. Open `index.html` in a browser.
3. For a local web server, run `python -m http.server 8000` from this folder and visit `http://localhost:8000`.

## Before submission
Personalize the sample content:
- Replace `Alex Morgan` with your name.
- Update the About section and project descriptions.
- Change `hello@example.com` to your email.
- Update the social profile links.
- Optional: add your own real project links.

## Host on Amazon S3 (static website)

> AWS Console labels can change slightly over time. Do not put secrets or private information in a public website bucket.

1. Sign in to the AWS Management Console and open **Amazon S3**.
2. Choose **Create bucket**. Use a globally unique name such as `your-name-portfolio-2026`; choose your preferred AWS Region.
3. For the simplest S3 website-endpoint setup, clear **Block all public access** and acknowledge the warning. Only do this for a bucket intended to host public static website files. An alternative is to keep the bucket private and use CloudFront with Origin Access Control.
4. Create the bucket.
5. Open the bucket → **Properties** → **Static website hosting** → **Edit**.
6. Choose **Use this bucket to host a website**, enable it, and set the index document to `index.html`. Save.
7. Open **Permissions** → **Bucket policy** and add the policy below, replacing `YOUR_BUCKET_NAME` with your exact bucket name:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForWebsiteFiles",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
```

8. Open **Objects** → **Upload**. Upload `index.html`, `style.css`, and `script.js` (upload the files themselves, not the ZIP).
9. Return to **Properties** → **Static website hosting** and open the **Bucket website endpoint**.
10. Test the page on desktop and mobile. If changes do not appear, refresh the browser cache.

### Important AWS notes
- An S3 website endpoint is public HTTP, not HTTPS. For HTTPS and a custom domain, use Amazon CloudFront (with a private S3 origin where possible) and optionally Route 53 / ACM.
- If your organization or AWS account enforces Block Public Access, the public-bucket approach may be denied. Use CloudFront with Origin Access Control instead.
- S3 website hosting serves static files; it does not run backend code or process a contact form. This sample uses a `mailto:` link for contact.
- AWS may charge for storage, requests, and data transfer according to your account and usage.

## Useful official AWS documentation
- S3 static website hosting: https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
- Configuring a bucket for website hosting: https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html
- Making objects public / bucket policy: https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html
- CloudFront with S3: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.SimpleDistribution.html
