# Password-Strength-Checker-Tool

Website Tool to build and Check Strong Password!

Complete, production-ready, static Password Strength Checker website that you can host directly on AWS S3 — no backend needed, secure, mobile-friendly, served securely over HTTPS via Cloudflare.

This Website Tool is My First Project Using AWS S3 Service for hosting static website served securely over HTTPS.

🎯 Features
Real-time password strength meter (using zxcvbn, same library used by Dropbox)
Visual feedback (color-coded strength bar)
Shows estimated crack time
Warns about common passwords, repetition, patterns
Clean, modern UI with Tailwind CSS (via CDN — no build step)
100% static — perfect for S3 hosting
No external tracking or cookies — privacy-friendly


📁 File Structure for S3
You’ll upload just one file:

index.html 
That’s it! ✅


🚀 How to Deploy to AWS S3

✅ STEP 1: Prepare Your S3 Bucket (if not already done)
Go to AWS S3 Console
Create a new bucket (e.g., my-password-checker-2025)
Enable Static Website Hosting in bucket properties
Index document: index.html
Upload index.html to the bucket
Set bucket policy for public read (if not already):

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

✅ STEP 2: Add Your Domain to Cloudflare
1. Go to Cloudflare Dashboard
2. Click “Add a Site”
3. Enter: dpdns.org (the root domain — Cloudflare manages DNS at zone level)
💡 Even though you want fhkprojects.dpdns.org, you must add the root zone dpdns.org. 

4. Click “Add Site”
5. Choose plan: Free Plan (more than enough for static site)
6. Cloudflare will scan existing DNS records — review and keep/delete as needed
7. Click “Continue”
8. Cloudflare will assign you two Cloudflare nameservers (e.g., lara.ns.cloudflare.com, rob.ns.cloudflare.com)

✅ STEP 3: Update Nameservers at Your Domain Registrar
Wherever you bought/registered dpdns.org (e.g., GoDaddy, Namecheap, AWS Route 53, etc.) 

➤ Replace current nameservers with the two Cloudflare nameservers shown.
Example:
lara.ns.cloudflare.com
rob.ns.cloudflare.com

✅ Save changes.

⏳ DNS propagation may take 5 mins to 24 hours (usually <1 hour).

You can check progress in Cloudflare → Overview → “Nameservers are active” ✅

✅ STEP 4: Create DNS Record in Cloudflare for Your Subdomain
1. In Cloudflare Dashboard → Select dpdns.org
2. Go to DNS → Records
3. Click “Add Record”
Type: CNAME
Name: fhkprojects
Target: [your-bucket].s3-website-[region].amazonaws.com
(e.g., my-bucket.s3-website-us-east-1.amazonaws.com)
Proxy status: ✅ Proxied (orange cloud) — THIS IS IMPORTANT!
TTL: Auto
✅ Click “Save”

🟠 Make sure the cloud icon is ORANGE — that means traffic flows through Cloudflare (so SSL and redirects work).

✅ STEP 5: Enforce HTTPS + Redirect in Cloudflare
1. Go to Rules → Page Rules (optional, but we’ll use SSL/TLS settings instead — simpler)
2. Go to SSL/TLS → Overview
Set SSL/TLS encryption mode to: Flexible
💡 “Flexible” = Cloudflare uses HTTPS to browser, but HTTP to S3 (perfect for S3 static sites) 
3. Go to SSL/TLS → Edge Certificates
✅ Enable “Always Use HTTPS” → This forces HTTP → HTTPS redirect automatically
✅ Enable “Automatic HTTPS Rewrites” (optional — helps with mixed content)
✅ STEP 6: (Optional) Cache Optimization for Static Site
Go to Rules → Page Rules → Create Page Rule

URL: fhkprojects.dpdns.org/*

Add settings:

✅ Cache Level → Cache Everything
✅ Edge Cache TTL → 1 day (or longer)
✅ Browser Cache TTL → 1 month
✅ Save and Deploy

This makes your static site load faster globally 🚀 

✅ STEP 7: Test Your Site!
✅ Visit in browser:

http://fhkprojects.dpdns.org → should auto-redirect to https://
https://fhkprojects.dpdns.org → should load your S3 site with padlock 🔒

✅ Test in terminal:
curl -I http://fhkprojects.dpdns.org
# Should return 301 Moved Permanently → Location: https://...

curl -I https://fhkprojects.dpdns.org
# Should return 200 OK

✅ Check security: Click padlock in browser → “Connection is secure”


✅ Why This Is Safe & Responsible
🔒 No passwords leave the browser — everything runs client-side
🧠 Uses zxcvbn — industry standard (used by Dropbox, Cloudflare, etc.)
📱 Responsive design — works on phones and desktops
🌐 No external dependencies except CDN-hosted libraries (Tailwind + zxcvbn)
🚫 No tracking, no cookies, no analytics — respects user privacy
🔒 Served securely over HTTPS via Cloudflare.


🎉 You’re Done!
Your static website is now:

✅ Served securely over HTTPS via Cloudflare
✅ Accessible at https://fhkprojects.dpdns.org
✅ Automatically redirects HTTP → HTTPS
✅ Backed by S3 (cheap, durable, simple)
✅ Protected by Cloudflare (CDN, security, caching)
✅ Zero cost for SSL and basic features (Free Plan)
