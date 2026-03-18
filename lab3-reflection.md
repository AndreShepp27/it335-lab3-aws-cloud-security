# Lab 3 Reflection – AWS Cloud Security Fundamentals

## Summary of Configurations

In this lab I set up four main security controls in AWS: identity management (IAM), secure storage (S3), a secured virtual computer (EC2), and monitoring tools like CloudTrail and Billing. Each of these controls connects directly to mistakes that were made in the 2019 Capital One breach, where a hacker named Paige Thompson stole data from over 106 million people by taking advantage of poor cloud security settings.

## IAM – Identity and Access Management

The first thing I did was check that the root account had Multi-Factor Authentication (MFA) turned on, which it did. MFA means that even if someone gets your password, they still cannot log in without a second verification step. Then I created a new user called lab-student-user and put them in a group called LabUsers. I attached a policy to that group that only allows read-only access to a few basic services. When I logged in as that user and tried to create an S3 bucket, it said permission failed which confirmed the restrictions were working.

In the Capital One breach, the attacker got access to an IAM role that had way more permissions than it needed. Because of that, she was able to access and copy huge amounts of data. If Capital One had used least privilege like I did in this lab, the attacker would have been stopped much sooner because the stolen credentials would not have had enough permissions to do serious damage.

## S3 – Secure Storage

I created a private S3 bucket with all public access blocked. This means nobody from the internet can access the files in that bucket, even by accident. I confirmed this by checking the Permissions tab which showed all four block settings were turned on.

In the Capital One breach, the attacker used stolen credentials to copy nearly 30 GB of sensitive data straight out of S3 buckets. If public access had been fully blocked and bucket permissions had been tighter, it would have been much harder to pull that data out. This is one of the simplest settings to turn on in AWS and it makes a huge difference.

## EC2 – Secured Compute

I launched a free tier virtual machine and set up a security group that only allows SSH connections from my specific IP address. This means nobody else on the internet can even attempt to connect to the machine. I also checked the Instance Metadata Service settings and made sure IMDSv2 was set to Required instead of Optional.

This is very relevant to the Capital One breach. The attacker exploited something called Server-Side Request Forgery (SSRF) to trick the server into calling the AWS metadata service, which then handed over temporary login credentials. IMDSv1 allowed this attack to work easily. IMDSv2 requires an extra session token step that makes this kind of attack much harder to pull off. Restricting the security group also means an attacker cannot even reach the server in the first place.

## Visibility and Governance – CloudTrail and Billing

I navigated to CloudTrail and saw that it was already logging every action taken in my AWS account, including everything I did in this lab like creating users, buckets, and instances. I also checked the Billing dashboard to see my current usage and make sure I stayed within Free Tier limits.

One of the biggest failures in the Capital One breach was that the attack went undetected from March 2019 all the way to July 2019, about four months. The only reason it was caught was because someone sent a tip to Capital Ones responsible disclosure email. If Capital One had been actively monitoring CloudTrail logs for unusual activity like someone suddenly syncing gigabytes of S3 data, they could have caught the breach in hours instead of months. Continuous monitoring closes the window of opportunity that attackers rely on.

## Critical Analysis

Out of all the controls I set up, blocking public S3 access felt the most straightforward and most impactful. It is a simple checkbox that prevents a huge category of data leaks. The trickiest part was the IAM policy because it is easy to accidentally give too many permissions or too few. Security groups were also easy to misconfigure since the tempting default is to open access to everyone which means anyone in the world can try to connect.

The bigger lesson from Capital One is that having the right tools available is not enough. AWS offered all of these security features back in 2019 when the breach happened. The problem was that nobody at Capital One made sure they were configured correctly. That is an organizational and cultural failure, not just a technical one. Companies need to treat cloud security configuration as an ongoing responsibility, not a one-time setup task. Regular audits, automated compliance checks, and a security-first culture are what actually keep these controls in place over time.
