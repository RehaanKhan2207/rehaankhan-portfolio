AWS Static Portfolio Website Deployment
A highly resilient, globally distributed, and secure static single-page portfolio hosted on AWS and delivered over HTTPS.  

Live Deployment Link
Secure CDN URL: https://d1eqmut0kkczwg.cloudfront.net

GitHub Code Repository:(https://github.com/RehaanKhan2207/rehaankhan-portfolio)

Architectural Summary
Origin Layer: Amazon S3 (rehaankhan1-portfolio bucket) in the ap-south-2 (Mumbai) region.

CDN Layer: Amazon CloudFront (Distribution ID: E3PA233NS5S4XD).

Default Root Object: index.html.  

Transport Security: HTTP requests are automatically upgraded and redirected to HTTPS.

Access Control: Amazon S3 Block Public Access is fully enabled. Direct S3 URL bypass is blocked via a secure S3 Bucket Policy configured with CloudFront Origin Access Control (OAC).

Deployment Steps & Commands Used
Local Version Control:bash
git init
git add index.html styles.css
git commit -m "feat: implement portfolio template"
git remote add origin https://github.com/RehaanKhan2207/rehaankhan-portfolio.git
git push -u origin main


AWS S3 Deployment:

Provisioned an S3 bucket named rehaankhan1-portfolio.  

Synchronized local assets using the AWS CLI :  

Bash
aws s3 sync. s3://rehaankhan1-portfolio --exclude ".git/*" --exclude "policy.json"
CloudFront CDN Setup:

Created a global distribution pointing to the regional S3 REST endpoint.

Enabled Origin Access Control (OAC) to secure S3 object access.  

Enforced HTTP to HTTPS redirection.  

Set the Default Root Object to index.html.

Bucket Hardening & Access Control:

Saved the secure CloudFront access policy locally as policy.json.  

Applied the bucket policy via the CLI :  

Bash
aws s3api put-bucket-policy --bucket rehaankhan1-portfolio --policy file://policy.json
Enabled "Block All Public Access" in S3 to prevent direct origin bypass.
