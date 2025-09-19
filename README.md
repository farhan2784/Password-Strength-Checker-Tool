Password Strength Checker Tool
A lightweight, secure, and mobile-friendly static website to evaluate password strength and generate robust passwords, hosted on AWS S3 and served over HTTPS via Cloudflare.
This project marks my first experience hosting a static website on AWS S3, leveraging Cloudflare for secure, high-performance delivery.

🎯 Features
Real-Time Password Strength Meter: Powered by zxcvbn (used by Dropbox) for accurate strength evaluation.
Visual Feedback: Color-coded strength bar for intuitive user experience.
Crack Time Estimation: Displays estimated time to crack the password.
Password Warnings: Alerts for common passwords, repetitive characters, or predictable patterns.
Modern UI: Clean, responsive design built with Tailwind CSS (CDN-based, no build step required).
Fully Static: Ideal for AWS S3 hosting with no backend dependencies.
Privacy-Focused: No external tracking, cookies, or analytics for maximum user privacy.

📁 File Structure for S3
Only one file is needed for deployment:

index.html

That's all! ✅
🚀 Deployment Guide for AWS S3 and Cloudflare
✅ Step 1: Set Up Your S3 Bucket

Navigate to the AWS S3 Console.
Create a new bucket (e.g., my-password-checker-2025).
Enable Static Website Hosting in bucket properties.
Set Index document to index.html.


Upload index.html to the bucket.
Configure the bucket policy for public read access:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}

✅ Step 2: Add Your Domain to Cloudflare

Go to the Cloudflare Dashboard and click Add a Site.
Enter your root domain (e.g., dpdns.org).
Note: Add the root domain (dpdns.org), not the subdomain (fhkprojects.dpdns.org).


Select the Free Plan (sufficient for static sites).
Review Cloudflare’s scan of existing DNS records and keep or delete as needed.
Note the two Cloudflare nameservers assigned (e.g., lara.ns.cloudflare.com, rob.ns.cloudflare.com).

✅ Step 3: Update Nameservers at Your Domain Registrar

Log in to your domain registrar (e.g., GoDaddy, Namecheap, AWS Route 53).
Replace the current nameservers with Cloudflare’s nameservers (e.g., lara.ns.cloudflare.com, rob.ns.cloudflare.com).
Save changes.
Allow 5 minutes to 24 hours for DNS propagation (typically under 1 hour).
Verify in Cloudflare’s Overview tab: “Nameservers are active” ✅.

✅ Step 4: Create a DNS Record in Cloudflare

In the Cloudflare Dashboard, select dpdns.org.
Navigate to DNS > Records and click Add Record.
Configure:
Type: CNAME
Name: fhkprojects
Target: [your-bucket].s3-website-[region].amazonaws.com (e.g., my-password-checker-2025.s3-website-us-east-1.amazonaws.com)
Proxy status: ✅ Proxied (orange cloud icon)
TTL: Auto

Click Save.
Important: Ensure the cloud icon is orange to route traffic through Cloudflare for SSL and performance.

✅ Step 5: Enforce HTTPS in Cloudflare
Go to SSL/TLS > Overview.
Set SSL/TLS encryption mode to Flexible (HTTPS to browser, HTTP to S3).
In SSL/TLS > Edge Certificates:
Enable Always Use HTTPS for automatic HTTP-to-HTTPS redirects.
Enable Automatic HTTPS Rewrites to fix mixed content issues (optional).

✅ Step 6: Optimize Caching (Optional)
Go to Rules > Page Rules and create a new rule.
Set URL to fhkprojects.dpdns.org/*.
Add settings:
Cache Level: Cache Everything
Edge Cache TTL: 1 day (or longer)
Browser Cache TTL: 1 month

Click Save and Deploy for faster global loading.

✅ Step 7: Test Your Site
Visit http://fhkprojects.dpdns.org (should redirect to HTTPS).
Visit https://fhkprojects.dpdns.org (should load with a padlock 🔒).
Test via terminal:curl -I http://fhkprojects.dpdns.org
# Should return 301 Moved Permanently → Location: https://...
curl -I https://fhkprojects.dpdns.org
# Should return 200 OK

Verify security in your browser: Click the padlock to confirm “Connection is secure.”

✅ Why This Setup Is Secure and Responsible

Client-Side Processing: Passwords never leave the browser, ensuring privacy.
Industry-Standard Library: Uses zxcvbn (trusted by Dropbox and Cloudflare).
Responsive Design: Works seamlessly on mobile and desktop devices.
Minimal Dependencies: Relies only on CDN-hosted Tailwind CSS and zxcvbn.
Privacy-First: No tracking, cookies, or analytics.
Secure Delivery: Served over HTTPS via Cloudflare for encryption and protection.

🎉 Congratulations!
Your Password Strength Checker is now live at https://fhkprojects.dpdns.org! It’s:

Secure: Delivered over HTTPS via Cloudflare.
Accessible: Automatically redirects HTTP to HTTPS.
Cost-Effective: Hosted on AWS S3 with Cloudflare’s Free Plan.
High-Performance: Optimized with global CDN and caching.
Durable: Backed by S3’s reliable storage.

Enjoy your secure, user-friendly, and privacy-focused static website! 🚀
