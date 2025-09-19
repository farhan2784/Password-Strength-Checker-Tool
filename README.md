# Password-Strength-Checker-Tool

Website Tool to build and Check Strong Password!

Complete, production-ready, static Password Strength Checker website that you can host directly on AWS S3 — no backend needed, secure, mobile-friendly, and educational.

This Website Tool is my first project using AWS S3 Service for hosting static website.

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
Step 1: Save the file
Save the above code as index.html on your computer.

Step 2: Upload to S3
Go to AWS S3 Console
Create a new bucket (e.g., my-password-checker-2025)
Enable Static Website Hosting in bucket properties
Index document: index.html
Upload index.html to the bucket
Set bucket policy for public read (if not already):

json
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


