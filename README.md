# AWS Cloud Computing - Complete Beginner's Guide

> A detailed, step-by-step guide for engineering students covering three core AWS services: **S3 Static Hosting**, **EC2 with NGINX/Apache**, and **AWS Lambda + API Gateway**.
>
> All instructions are for the **AWS Free Tier** account.

---

## Table of Contents

1. [What is Cloud Computing?](#1-what-is-cloud-computing)
2. [What is AWS?](#2-what-is-aws)
3. [Setting Up Your Free AWS Account](#3-setting-up-your-free-aws-account)
4. [Topic 1: Host a Static HTML Webpage Using Amazon S3](#4-topic-1-host-a-static-html-webpage-using-amazon-s3)
5. [Topic 2: Launch an EC2 Instance, SSH Into It, and Deploy NGINX/Apache](#5-topic-2-launch-an-ec2-instance-ssh-into-it-and-deploy-nginxapache)
6. [Topic 3: Configure a Simple API Using AWS Lambda and API Gateway](#6-topic-3-configure-a-simple-api-using-aws-lambda-and-api-gateway)
7. [Summary & Comparison Table](#7-summary--comparison-table)
8. [Common Mistakes to Avoid](#8-common-mistakes-to-avoid)
9. [Useful Resources](#9-useful-resources)

---

## 1. What is Cloud Computing?

### Simple Definition

Cloud Computing means **using someone else's powerful computers over the internet** instead of buying and maintaining your own.

### Real-Life Examples (That Everyone Can Understand)

| Everyday Example | Cloud Equivalent |
|---|---|
| Renting a house instead of building one | Using AWS servers instead of buying your own |
| Using Uber instead of buying a car | Using cloud services instead of owning hardware |
| Storing photos on Google Photos instead of a hard drive | Using cloud storage (like S3) |
| Ordering food from Zomato instead of cooking | Using ready-made cloud services instead of building everything yourself |
| Using a gym instead of buying gym equipment | Using cloud computing power instead of buying servers |

### Why Do Companies Use Cloud Computing?

Imagine you're opening a **chai stall**:

- **Without Cloud (Old Way):** You buy a huge shop, 50 chairs, 10 stoves - even though initially only 5 customers come daily. You spent lakhs of rupees upfront.
- **With Cloud (New Way):** You rent a small space, 5 chairs, 1 stove. When more customers come (like during exams), you rent more chairs and stoves. When business is slow, you return the extra stuff and pay less.

**This is exactly what cloud computing does for websites and apps!**

### Three Types of Cloud Services

Think of it like **transportation**:

1. **IaaS (Infrastructure as a Service)** - Like renting a car (you drive it yourself)
   - Example: **EC2** - You get a raw computer, you install everything
   - You control: Everything from OS to applications

2. **PaaS (Platform as a Service)** - Like taking an Uber (someone drives, you just say where to go)
   - Example: **Elastic Beanstalk** - You just give your code, AWS handles the rest
   - You control: Just your application code

3. **SaaS (Software as a Service)** - Like watching Netflix (everything is done for you)
   - Example: **Gmail, Google Docs** - Just open and use
   - You control: Just your data

### Key Benefits of Cloud Computing

```
1. No upfront cost     - Pay only for what you use (like electricity bill)
2. Scalability         - Handle 10 users or 10 million users easily
3. Global reach        - Deploy your app worldwide in minutes
4. Reliability         - AWS has 99.99% uptime guarantee
5. Security            - AWS spends billions on security (more than any single company can)
```

---

## 2. What is AWS?

### Simple Definition

**AWS (Amazon Web Services)** is the world's largest cloud platform, offered by Amazon (yes, the same Amazon where you buy products online!).

### A Brief History

- **2006:** Amazon realized they had massive extra computing power from running Amazon.com, so they started renting it out. AWS was born!
- **Today:** AWS has **200+ services** and is used by Netflix, Airbnb, NASA, and millions of companies worldwide.

### AWS Services We'll Learn Today

| Service | What It Does | Real-Life Analogy |
|---|---|---|
| **S3** | Stores files (images, HTML, videos) | A digital locker/cupboard |
| **EC2** | Gives you a virtual computer | Renting a computer from a cyber cafe |
| **Lambda** | Runs your code without a server | A vending machine (put money in, get result out) |
| **API Gateway** | Creates an API endpoint (URL) | A reception desk that directs visitors |

---

## 3. Setting Up Your Free AWS Account

### What You Get Free (For 12 Months)

- **EC2:** 750 hours/month of t2.micro (1 CPU, 1 GB RAM)
- **S3:** 5 GB of storage
- **Lambda:** 1 million requests/month
- **API Gateway:** 1 million API calls/month

### Step-by-Step: Creating Your AWS Free Tier Account

1. **Go to** [https://aws.amazon.com/free](https://aws.amazon.com/free)

2. **Click** "Create a Free Account"

3. **Enter your details:**
   - Email address (use your college email or personal email)
   - Password (make it strong!)
   - AWS account name (e.g., "MyLearningAccount")

4. **Choose** "Personal" account type

5. **Enter your personal information:**
   - Full name
   - Phone number
   - Address (your home address is fine)

6. **Payment Information:**
   - You MUST enter a credit/debit card
   - AWS will charge **Rs. 2 (or $1)** as verification (this is refunded!)
   - **Don't worry - you won't be charged if you stay within free tier limits**

7. **Identity Verification:**
   - AWS will call or text you with a verification code
   - Enter the code

8. **Select Support Plan:**
   - Choose **"Basic Support - Free"** (this is important!)

9. **Done!** You'll receive a confirmation email.

### Important Safety Tips

```
WARNING: Set up billing alerts to avoid unexpected charges!

Go to: AWS Console > Billing > Budgets > Create Budget
Set a budget of $0 (or $1) so you get an email if you're about to be charged.
```

---

## 4. Topic 1: Host a Static HTML Webpage Using Amazon S3

### What is Amazon S3?

**S3 = Simple Storage Service**

Think of S3 as a **Google Drive on steroids**. It stores files - but unlike Google Drive, it can also **serve those files as a website** to anyone on the internet!

### Real-Life Analogy

Imagine you made a beautiful **poster** for a college fest:

- **Without S3:** You make 1000 photocopies and hand them to everyone. Expensive and slow.
- **With S3:** You upload the poster to S3, share the link, and ANYONE in the world can see it. No photocopying needed!

### Key S3 Concepts

| Concept | Meaning | Analogy |
|---|---|---|
| **Bucket** | A container that holds your files | A folder on your computer |
| **Object** | Any file stored in a bucket (HTML, image, video) | A file inside the folder |
| **Bucket Name** | A globally unique name for your bucket | Like a website domain name - no two can be the same |
| **Region** | The physical location of the AWS data center | Like choosing which city to store your stuff in |

### What is a "Static Website"?

- **Static Website:** The content doesn't change based on who visits. Everyone sees the same page. Like a **printed brochure**.
  - Examples: Portfolio websites, company landing pages, documentation sites
  - Technologies: HTML, CSS, JavaScript (frontend only)

- **Dynamic Website:** Content changes based on the user. Like a **personalized newspaper**.
  - Examples: Facebook (everyone sees different feed), Amazon (personalized recommendations)
  - Technologies: Needs a backend server (Node.js, Python, etc.)

**S3 can only host STATIC websites!**

### Step-by-Step: Hosting a Static Website on S3

#### Step 1: Create Your HTML File

First, create a simple HTML file on your computer. Save this as `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First AWS Website</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
        }
        .container {
            text-align: center;
            padding: 40px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            backdrop-filter: blur(10px);
        }
        h1 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }
        p {
            font-size: 1.2rem;
            margin-bottom: 10px;
        }
        .highlight {
            color: #ffd700;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hello from AWS S3!</h1>
        <p>This website is hosted on <span class="highlight">Amazon S3</span></p>
        <p>Built by: <span class="highlight">Your Name Here</span></p>
        <p>College: <span class="highlight">Your College Name</span></p>
        <p>Date: <span class="highlight">April 2026</span></p>
    </div>
</body>
</html>
```

Also create an `error.html` file (for when someone visits a wrong page):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Page Not Found</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding-top: 100px;
            background-color: #f0f0f0;
        }
        h1 { color: #e74c3c; font-size: 3rem; }
        p { font-size: 1.2rem; color: #555; }
        a { color: #3498db; text-decoration: none; }
    </style>
</head>
<body>
    <h1>404 - Page Not Found</h1>
    <p>Oops! The page you're looking for doesn't exist.</p>
    <p><a href="index.html">Go back to Home</a></p>
</body>
</html>
```

#### Step 2: Log In to AWS Console

1. Go to [https://console.aws.amazon.com](https://console.aws.amazon.com)
2. Enter your email and password
3. You'll see the **AWS Management Console** (the main dashboard)

#### Step 3: Navigate to S3

1. In the **search bar** at the top, type **"S3"**
2. Click on **"S3"** from the results
3. You'll see the S3 dashboard (it might be empty if this is your first time)

#### Step 4: Create a New S3 Bucket

1. Click the **"Create bucket"** button (orange button)

2. **Bucket name:** Enter a globally unique name
   - Example: `my-first-website-yourname-2026` (replace "yourname" with your actual name)
   - Rules: Only lowercase letters, numbers, and hyphens. No spaces!
   - **This name must be unique across ALL of AWS** (not just your account)

3. **AWS Region:** Select **Asia Pacific (Mumbai) ap-south-1** (closest to India for faster loading)

4. **Object Ownership:** Select **"ACLs disabled (recommended)"**

5. **Block Public Access settings:**
   - **UNCHECK** the box that says "Block all public access"
   - A warning will appear - **check the acknowledgment box** that says "I acknowledge that the current settings might result in this bucket and the objects within becoming public"
   - **Why?** Because we WANT people to see our website! If we block public access, no one can view it.

6. **Bucket Versioning:** Leave as "Disable" (not needed for this demo)

7. **Tags:** Optional, you can skip this

8. **Default encryption:** Leave as default (SSE-S3)

9. Click **"Create bucket"**

**Congratulations! Your bucket is created!**

#### Step 5: Upload Your Files

1. Click on your newly created bucket name
2. Click the **"Upload"** button
3. Click **"Add files"**
4. Select both `index.html` and `error.html` from your computer
5. Click **"Upload"** at the bottom
6. Wait for the upload to complete, then click **"Close"**

#### Step 6: Enable Static Website Hosting

1. In your bucket, go to the **"Properties"** tab (at the top)
2. Scroll ALL the way down to **"Static website hosting"**
3. Click **"Edit"**
4. Select **"Enable"**
5. **Hosting type:** Select "Host a static website"
6. **Index document:** Type `index.html`
7. **Error document:** Type `error.html`
8. Click **"Save changes"**

**Important:** After saving, you'll see a **Bucket website endpoint** URL like:
```
http://my-first-website-yourname-2026.s3-website.ap-south-1.amazonaws.com
```
**Copy this URL** - this is your website address!

#### Step 7: Add a Bucket Policy (Make Files Public)

Even though we unblocked public access, we still need to explicitly allow people to READ our files.

1. Go to the **"Permissions"** tab
2. Scroll down to **"Bucket policy"**
3. Click **"Edit"**
4. Paste this JSON policy (replace `YOUR-BUCKET-NAME` with your actual bucket name):

```json
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
```

**What does this policy mean?**

| Part | Meaning |
|---|---|
| `"Effect": "Allow"` | We're ALLOWING something |
| `"Principal": "*"` | For EVERYONE (the * means anyone) |
| `"Action": "s3:GetObject"` | They can READ/DOWNLOAD files |
| `"Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"` | From this specific bucket, all files (`/*`) |

5. Click **"Save changes"**

#### Step 8: Test Your Website!

1. Go back to **Properties** tab
2. Scroll down to **Static website hosting**
3. Click on the **Bucket website endpoint** URL
4. **Your website is LIVE on the internet!**

Share this URL with your friends - they can access it from anywhere in the world!

### How It Works (Behind the Scenes)

```
User types URL in browser
        |
        v
Request goes to AWS S3
        |
        v
S3 finds the bucket
        |
        v
S3 serves index.html
        |
        v
User sees your website!
```

### S3 Free Tier Limits

| Feature | Free Limit |
|---|---|
| Storage | 5 GB |
| GET requests (page views) | 20,000/month |
| PUT requests (uploads) | 2,000/month |
| Data transfer out | 100 GB/month |

**For a simple portfolio website, you'll NEVER exceed these limits!**

### Cleanup (When You're Done Practicing)

To avoid any charges:
1. Go to your bucket
2. Select all objects > **Delete**
3. Go back to S3 dashboard
4. Select your bucket > **Delete**
5. Type the bucket name to confirm deletion

---

## 5. Topic 2: Launch an EC2 Instance, SSH Into It, and Deploy NGINX/Apache

### What is Amazon EC2?

**EC2 = Elastic Compute Cloud**

EC2 gives you a **virtual computer** (called an "instance") running in AWS's data center. You can do anything with it - install software, host websites, run applications, etc.

### Real-Life Analogy

Think of it like a **cyber cafe**:

- **Without EC2:** You buy a computer (Rs. 50,000+), set it up at home, pay for electricity, handle repairs, ensure it runs 24/7. Expensive and stressful!
- **With EC2:** You "rent" a computer from AWS for a few rupees per hour (or FREE with free tier!). AWS handles electricity, cooling, repairs, and security. You just use it remotely!

### Key EC2 Concepts

| Concept | Meaning | Analogy |
|---|---|---|
| **Instance** | A virtual computer | A computer in a cyber cafe |
| **AMI (Amazon Machine Image)** | Pre-configured OS template | Like a Windows installation disc |
| **Instance Type** | Computer specifications (CPU, RAM) | Like choosing between a basic laptop vs gaming laptop |
| **Key Pair** | SSH login credentials (like a password file) | Like the key to a locker |
| **Security Group** | Firewall rules (who can access) | Like a security guard at a building gate |
| **Elastic IP** | A permanent IP address | Like a permanent phone number |

### What are NGINX and Apache?

Both are **web servers** - software that serves web pages to users.

| Feature | NGINX | Apache |
|---|---|---|
| **Pronunciation** | "Engine-X" | "A-pah-chee" |
| **Created** | 2004 by Igor Sysoev | 1995 by Apache Foundation |
| **Performance** | Faster for static content | Better for dynamic content |
| **Config style** | Simple, directive-based | Uses .htaccess files |
| **Used by** | Netflix, Airbnb, WordPress.com | Apple, Adobe, PayPal |
| **Market share** | ~34% of websites | ~31% of websites |

### What is SSH?

**SSH = Secure Shell**

SSH lets you **remotely control another computer** using your terminal/command prompt. It's like using TeamViewer, but through text commands.

```
Your Computer  ----SSH connection (encrypted)---->  EC2 Instance
(your laptop)                                       (AWS computer)
```

### Step-by-Step: Launching an EC2 Instance and Deploying NGINX

#### Step 1: Navigate to EC2

1. Log in to [AWS Console](https://console.aws.amazon.com)
2. In the search bar, type **"EC2"**
3. Click on **"EC2"** from results

#### Step 2: Launch an Instance

1. Click the **"Launch instance"** button (orange)

2. **Name and tags:**
   - Name: `my-first-webserver`

3. **Application and OS Images (AMI):**
   - Select **"Amazon Linux 2023"** (it's free tier eligible)
   - You'll see a "Free tier eligible" tag
   - Architecture: **64-bit (x86)**

   > **Why Amazon Linux?** It's optimized for AWS, lightweight, and free. You can also choose Ubuntu if you prefer.

4. **Instance type:**
   - Select **t2.micro** (Free tier eligible)
   - This gives you: 1 CPU, 1 GB RAM
   - You'll see "Free tier eligible" label

   > **Think of instance types like car models:**
   > - t2.micro = Bicycle (basic, free) - perfect for learning!
   > - t2.small = Scooter (a bit more power)
   > - m5.large = Car (good for production)
   > - c5.4xlarge = Sports car (high performance)

5. **Key pair (login):**
   - Click **"Create new key pair"**
   - Key pair name: `my-aws-key`
   - Key pair type: **RSA**
   - Private key file format:
     - If using Windows with PuTTY: Choose **.ppk**
     - If using Mac/Linux or Windows with Git Bash: Choose **.pem**
   - Click **"Create key pair"**
   - **The .pem file will download automatically. SAVE THIS FILE SAFELY! You cannot download it again!**

6. **Network settings:**
   - Click **"Edit"** (on the right side)
   - **VPC:** Leave default
   - **Subnet:** Leave default
   - **Auto-assign public IP:** Make sure it's **"Enable"**
   - **Security Group:** Create a new security group
     - Security group name: `my-webserver-sg`
     - Description: `Allow SSH and HTTP access`
   - **Inbound Security Group Rules:**

     **Rule 1 (already there):**
     - Type: **SSH**
     - Port: **22**
     - Source: **Anywhere (0.0.0.0/0)** (for learning; in production, restrict this!)

     **Rule 2 (Click "Add security group rule"):**
     - Type: **HTTP**
     - Port: **80**
     - Source: **Anywhere (0.0.0.0/0)**

     **Rule 3 (Click "Add security group rule"):**
     - Type: **HTTPS**
     - Port: **443**
     - Source: **Anywhere (0.0.0.0/0)**

   > **What are these ports?**
   > - Port 22 (SSH): Like the door for remote control
   > - Port 80 (HTTP): Like the door for website visitors
   > - Port 443 (HTTPS): Like the secure door for website visitors

7. **Configure storage:**
   - Leave default: **8 GB, gp3** (free tier allows up to 30 GB)

8. **Advanced details:**
   - Leave everything as default for now

9. Click **"Launch instance"**

10. You'll see "Successfully initiated launch of instance"
11. Click on the **instance ID** link to go to your instance

#### Step 3: Wait for the Instance to Start

1. In the EC2 dashboard, you'll see your instance
2. Wait until **Instance state** shows **"Running"** (green)
3. Wait until **Status check** shows **"2/2 checks passed"**
4. Note down the **Public IPv4 address** (e.g., `13.234.xx.xx`)

#### Step 4: Connect via SSH

##### Option A: Using AWS Console (Easiest - No Setup Needed!)

1. Select your instance (checkbox)
2. Click **"Connect"** button at the top
3. Choose **"EC2 Instance Connect"** tab
4. Click **"Connect"**
5. A terminal will open in your browser - you're now inside the EC2 instance!

##### Option B: Using Git Bash on Windows

1. Open **Git Bash** (download from [https://git-scm.com](https://git-scm.com) if you don't have it)

2. Navigate to where your key file is:
   ```bash
   cd ~/Downloads
   ```

3. Set proper permissions for the key file:
   ```bash
   chmod 400 my-aws-key.pem
   ```

4. Connect to your instance:
   ```bash
   ssh -i "my-aws-key.pem" ec2-user@YOUR-PUBLIC-IP
   ```
   Replace `YOUR-PUBLIC-IP` with your instance's public IP.

5. Type **"yes"** when asked about fingerprint
6. You're now connected!

##### Option C: Using PuTTY on Windows

1. Download PuTTY from [https://www.putty.org](https://www.putty.org)
2. Open PuTTY
3. Host Name: `ec2-user@YOUR-PUBLIC-IP`
4. Port: 22
5. Connection type: SSH
6. In the left panel: Connection > SSH > Auth > Credentials
7. Browse and select your `.ppk` file
8. Click **"Open"**
9. Click **"Accept"** for the security alert

##### Option D: Using Terminal on Mac/Linux

```bash
chmod 400 ~/Downloads/my-aws-key.pem
ssh -i "~/Downloads/my-aws-key.pem" ec2-user@YOUR-PUBLIC-IP
```

#### Step 5: Install and Start NGINX

Now that you're connected to the EC2 instance, run these commands:

```bash
# Update the system packages (like updating your phone apps)
sudo yum update -y

# Install NGINX web server
sudo yum install nginx -y

# Start NGINX
sudo systemctl start nginx

# Make NGINX start automatically when the server restarts
sudo systemctl enable nginx

# Check if NGINX is running
sudo systemctl status nginx
```

You should see **"active (running)"** in green!

#### Step 6: Test Your Web Server

1. Go back to the AWS Console
2. Copy your instance's **Public IPv4 address**
3. Open a new browser tab
4. Type: `http://YOUR-PUBLIC-IP` (e.g., `http://13.234.56.78`)
5. You should see the **NGINX Welcome Page!**

**Your web server is LIVE on the internet!**

#### Step 7: Deploy Your Own Custom HTML Page

```bash
# Navigate to the NGINX web directory
cd /usr/share/nginx/html

# Backup the default page
sudo mv index.html index.html.backup

# Create your own page
sudo nano index.html
```

Paste this content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My EC2 Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            color: white;
            text-align: center;
            padding-top: 100px;
            min-height: 100vh;
        }
        .container {
            background: rgba(255,255,255,0.1);
            max-width: 600px;
            margin: 0 auto;
            padding: 40px;
            border-radius: 15px;
        }
        h1 { color: #00d4ff; font-size: 2.5rem; }
        p { font-size: 1.2rem; line-height: 1.8; }
        .badge {
            display: inline-block;
            background: #00d4ff;
            color: #1a1a2e;
            padding: 5px 15px;
            border-radius: 20px;
            margin: 5px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hosted on AWS EC2!</h1>
        <p>This website is running on an NGINX server deployed on Amazon EC2</p>
        <p>
            <span class="badge">AWS</span>
            <span class="badge">EC2</span>
            <span class="badge">NGINX</span>
            <span class="badge">Linux</span>
        </p>
        <p>Server Region: Mumbai (ap-south-1)</p>
        <p>Deployed by: <strong>Your Name</strong></p>
    </div>
</body>
</html>
```

Save and exit:
- Press **Ctrl + X**
- Press **Y** (for yes)
- Press **Enter**

Now refresh your browser - you'll see YOUR custom page!

### Alternative: Installing Apache Instead of NGINX

If you prefer Apache over NGINX:

```bash
# Install Apache (called httpd on Amazon Linux)
sudo yum install httpd -y

# Start Apache
sudo systemctl start httpd

# Enable Apache to start on boot
sudo systemctl enable httpd

# Check status
sudo systemctl status httpd

# Apache serves files from this directory:
cd /var/www/html

# Create your page
sudo nano index.html
# (paste your HTML content and save)
```

### How It All Works Together (Architecture Diagram)

```
User's Browser
      |
      | (types http://YOUR-IP)
      v
Internet
      |
      v
AWS Security Group (checks: is port 80 open? YES!)
      |
      v
EC2 Instance (Amazon Linux)
      |
      v
NGINX/Apache Web Server (listening on port 80)
      |
      v
Reads /usr/share/nginx/html/index.html
      |
      v
Sends HTML back to user's browser
      |
      v
User sees the website!
```

### EC2 Free Tier Limits

| Feature | Free Limit |
|---|---|
| Instance type | t2.micro only |
| Hours per month | 750 hours (enough for 1 instance running 24/7) |
| Storage | 30 GB of EBS (SSD) |
| Data transfer out | 100 GB/month |
| Duration | 12 months from sign-up |

### Cleanup (IMPORTANT - To Avoid Charges!)

When you're done practicing:

1. Go to **EC2 Dashboard**
2. Select your instance
3. Click **Instance state** > **Terminate instance**
4. Confirm termination

> **Warning:** A stopped instance still incurs EBS storage charges. Always **terminate** (not just stop) when done practicing.

---

## 6. Topic 3: Configure a Simple API Using AWS Lambda and API Gateway

### What is AWS Lambda?

**Lambda** lets you run code **without managing any server**. You just write your function, upload it, and AWS handles everything else.

### Real-Life Analogy: The Vending Machine

| Vending Machine | AWS Lambda |
|---|---|
| You put in money | A request/trigger arrives |
| Machine processes your choice | Lambda runs your code |
| You get your drink | You get the result back |
| Machine is idle (no cost) | No charge when not running |
| No shopkeeper needed | No server to manage |

**Key Point:** You only pay when your code is actually running, not when it's idle!

### What is API Gateway?

**API Gateway** creates a **public URL (endpoint)** that people or apps can call to trigger your Lambda function.

### Real-Life Analogy: The Restaurant

```
Customer (User/App)
    |
    | "I want butter chicken"
    v
Waiter (API Gateway)           <-- Takes the order, routes it
    |
    | Passes order to kitchen
    v
Chef (Lambda Function)         <-- Does the actual work
    |
    | Prepares the dish
    v
Waiter (API Gateway)           <-- Brings the result back
    |
    v
Customer gets butter chicken!
```

- **API Gateway** = The waiter (takes requests, returns responses)
- **Lambda** = The chef (does the actual work)
- You don't need to own the restaurant building (server)!

### What is an API?

**API = Application Programming Interface**

An API is a way for two software applications to **talk to each other**.

Example:
```
Your Weather App ----"What's the weather in Mumbai?"----> Weather API
                                                              |
Your Weather App <---"32°C, Sunny, Humidity: 65%"-----------|
```

### What is Serverless?

**Serverless** doesn't mean "no servers." It means **YOU don't manage the servers**. AWS handles everything.

| Traditional Server | Serverless (Lambda) |
|---|---|
| You rent a full computer (EC2) | You just give your code |
| Runs 24/7 (even when idle) | Runs only when triggered |
| You pay per hour | You pay per execution |
| You manage updates, security | AWS manages everything |
| Like renting an apartment | Like staying at a hotel room |

### Step-by-Step: Creating a Lambda Function + API Gateway

We'll build a simple API that:
- Takes a student's name and marks
- Returns their grade and a message

#### Step 1: Navigate to Lambda

1. Log in to [AWS Console](https://console.aws.amazon.com)
2. Search for **"Lambda"** in the search bar
3. Click on **"Lambda"**

#### Step 2: Create a Lambda Function

1. Click **"Create function"** (orange button)

2. Choose **"Author from scratch"**

3. **Function name:** `studentGradeCalculator`

4. **Runtime:** Select **Python 3.12** (or latest Python version available)

   > **Why Python?** It's easy to read, widely used, and perfect for beginners. Lambda also supports Node.js, Java, Go, Ruby, and more.

5. **Architecture:** x86_64 (default)

6. **Permissions:**
   - Expand "Change default execution role"
   - Select **"Create a new role with basic Lambda permissions"**
   - This automatically creates a role that lets Lambda write logs

7. Click **"Create function"**

#### Step 3: Write the Lambda Function Code

1. After creation, you'll see the **Code editor**
2. Delete the existing code in `lambda_function.py`
3. Paste this code:

```python
import json

def lambda_handler(event, context):
    """
    A simple student grade calculator API.
    
    Input: Student name and marks (0-100)
    Output: Grade, percentage, and a motivational message
    """
    
    try:
        # Get the request body
        # API Gateway sends data in the 'body' field
        if event.get('body'):
            body = json.loads(event['body'])
        else:
            body = event  # For direct Lambda testing
        
        # Extract student name and marks
        student_name = body.get('name', 'Student')
        marks = body.get('marks', 0)
        
        # Validate marks
        if not isinstance(marks, (int, float)):
            return {
                'statusCode': 400,
                'headers': {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                'body': json.dumps({
                    'error': 'Marks must be a number between 0 and 100'
                })
            }
        
        if marks < 0 or marks > 100:
            return {
                'statusCode': 400,
                'headers': {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                'body': json.dumps({
                    'error': 'Marks must be between 0 and 100'
                })
            }
        
        # Calculate grade
        if marks >= 90:
            grade = 'A+'
            message = f'Outstanding performance, {student_name}! Keep it up!'
        elif marks >= 80:
            grade = 'A'
            message = f'Excellent work, {student_name}! Almost perfect!'
        elif marks >= 70:
            grade = 'B+'
            message = f'Great job, {student_name}! You are doing well!'
        elif marks >= 60:
            grade = 'B'
            message = f'Good effort, {student_name}! Keep pushing!'
        elif marks >= 50:
            grade = 'C'
            message = f'You passed, {student_name}! There is room for improvement.'
        elif marks >= 40:
            grade = 'D'
            message = f'Just passed, {student_name}. Work harder next time!'
        else:
            grade = 'F'
            message = f'Unfortunately failed, {student_name}. Do not give up, try again!'
        
        # Create response
        result = {
            'student_name': student_name,
            'marks': marks,
            'grade': grade,
            'message': message,
            'percentage': f'{marks}%'
        }
        
        return {
            'statusCode': 200,
            'headers': {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'  # Allow requests from any website
            },
            'body': json.dumps(result)
        }
    
    except Exception as e:
        return {
            'statusCode': 500,
            'headers': {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            'body': json.dumps({
                'error': f'Something went wrong: {str(e)}'
            })
        }
```

4. Click **"Deploy"** (this saves and deploys your code)

#### Step 4: Test Your Lambda Function

1. Click **"Test"** button (next to Deploy)
2. **Create a new test event:**
   - Event name: `testStudent`
   - Replace the JSON with:

```json
{
    "name": "Rahul",
    "marks": 85
}
```

3. Click **"Save"** then click **"Test"**

4. You should see a **green "Execution result: succeeded"** with output like:

```json
{
    "statusCode": 200,
    "headers": {
        "Content-Type": "application/json",
        "Access-Control-Allow-Origin": "*"
    },
    "body": "{\"student_name\": \"Rahul\", \"marks\": 85, \"grade\": \"A\", \"message\": \"Excellent work, Rahul! Almost perfect!\", \"percentage\": \"85%\"}"
}
```

**Your Lambda function works!**

#### Step 5: Create an API Gateway

Now let's create a public URL so anyone can call this function.

1. Go to the search bar, type **"API Gateway"**
2. Click on **"API Gateway"**

3. You'll see different API types. Choose:
   - **HTTP API** - Click **"Build"**

   > **Why HTTP API?** It's simpler, cheaper, and perfect for most use cases. REST API has more features but is more complex.

4. **Create an API:**
   - Click **"Add integration"**
   - Integration type: **Lambda**
   - AWS Region: Select your region (e.g., `ap-south-1`)
   - Lambda function: Select **`studentGradeCalculator`**
   - API name: `StudentGradeAPI`
   - Click **"Next"**

5. **Configure routes:**
   - Method: **POST**
   - Resource path: `/grade`
   - Integration target: `studentGradeCalculator`
   - Click **"Next"**

   > **What is a Route?**
   > A route is like a specific address within your API.
   > - `/grade` with POST = "Send student data and get grade"
   > - Think of it like rooms in a building: `/grade` is room 1, `/attendance` could be room 2

6. **Define stages:**
   - Stage name: Leave as `$default`
   - Auto-deploy: Leave enabled
   - Click **"Next"**

7. **Review and create:**
   - Review all settings
   - Click **"Create"**

#### Step 6: Get Your API URL

1. After creation, you'll see the **API dashboard**
2. On the left side, you'll see your **Invoke URL**, something like:
   ```
   https://abc123xyz.execute-api.ap-south-1.amazonaws.com
   ```
3. Your full API endpoint is:
   ```
   https://abc123xyz.execute-api.ap-south-1.amazonaws.com/grade
   ```

#### Step 7: Test Your API

##### Method 1: Using the Browser (for GET requests) or curl

Open **Git Bash** or **Terminal** and run:

```bash
curl -X POST https://YOUR-API-URL/grade \
  -H "Content-Type: application/json" \
  -d '{"name": "Priya", "marks": 92}'
```

You should get a response like:
```json
{
    "student_name": "Priya",
    "marks": 92,
    "grade": "A+",
    "message": "Outstanding performance, Priya! Keep it up!",
    "percentage": "92%"
}
```

##### Method 2: Using Postman (GUI Tool)

1. Download **Postman** from [https://www.postman.com/downloads/](https://www.postman.com/downloads/)
2. Open Postman
3. Create a new request:
   - Method: **POST**
   - URL: `https://YOUR-API-URL/grade`
   - Body tab > raw > JSON
   - Paste:
     ```json
     {
         "name": "Amit",
         "marks": 73
     }
     ```
4. Click **"Send"**
5. You'll see the response in the bottom panel!

##### Method 3: Using a Simple HTML Frontend

Create this HTML file on your computer and open it in a browser:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Grade Calculator</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
        }
        .card {
            background: rgba(255,255,255,0.1);
            padding: 40px;
            border-radius: 20px;
            width: 400px;
            backdrop-filter: blur(10px);
        }
        h1 { text-align: center; color: #00d4ff; }
        input, button {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: none;
            border-radius: 8px;
            font-size: 16px;
        }
        input { background: rgba(255,255,255,0.2); color: white; }
        input::placeholder { color: rgba(255,255,255,0.5); }
        button {
            background: #00d4ff;
            color: #0f0c29;
            font-weight: bold;
            cursor: pointer;
        }
        button:hover { background: #00b8d9; }
        .result {
            margin-top: 20px;
            padding: 20px;
            background: rgba(0,212,255,0.1);
            border-radius: 10px;
            display: none;
        }
        .grade { font-size: 3rem; text-align: center; }
    </style>
</head>
<body>
    <div class="card">
        <h1>Grade Calculator</h1>
        <p style="text-align:center; opacity:0.7;">Powered by AWS Lambda</p>
        <input type="text" id="name" placeholder="Enter student name">
        <input type="number" id="marks" placeholder="Enter marks (0-100)" min="0" max="100">
        <button onclick="getGrade()">Calculate Grade</button>
        <div class="result" id="result">
            <div class="grade" id="grade"></div>
            <p id="message"></p>
            <p id="percentage"></p>
        </div>
    </div>
    <script>
        async function getGrade() {
            const name = document.getElementById('name').value;
            const marks = parseInt(document.getElementById('marks').value);
            
            // REPLACE THIS URL with your actual API Gateway URL
            const apiUrl = 'https://YOUR-API-URL/grade';
            
            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ name, marks })
                });
                const data = await response.json();
                
                document.getElementById('grade').textContent = data.grade;
                document.getElementById('message').textContent = data.message;
                document.getElementById('percentage').textContent = 'Percentage: ' + data.percentage;
                document.getElementById('result').style.display = 'block';
            } catch (error) {
                alert('Error: ' + error.message);
            }
        }
    </script>
</body>
</html>
```

### How Lambda + API Gateway Works (Architecture)

```
User/App sends POST request
    |
    | POST /grade  {"name": "Rahul", "marks": 85}
    v
API Gateway (receives the request)
    |
    | Validates and forwards to Lambda
    v
Lambda Function (runs your Python code)
    |
    | Calculates grade, creates response
    v
API Gateway (sends response back)
    |
    | {"grade": "A", "message": "Excellent!"}
    v
User/App receives the response
```

### Lambda Free Tier Limits (ALWAYS FREE - Not Just 12 Months!)

| Feature | Free Limit |
|---|---|
| Requests | 1,000,000 per month |
| Compute time | 400,000 GB-seconds per month |
| API Gateway | 1,000,000 HTTP API calls per month |

**These are ALWAYS free, not just for 12 months!** That means even after your free tier expires, Lambda and API Gateway have a perpetual free tier.

### Cleanup

1. **Delete API Gateway:**
   - Go to API Gateway console
   - Select your API > Actions > Delete

2. **Delete Lambda Function:**
   - Go to Lambda console
   - Select your function > Actions > Delete

---

## 7. Summary & Comparison Table

| Feature | S3 Static Hosting | EC2 + NGINX/Apache | Lambda + API Gateway |
|---|---|---|---|
| **What it does** | Hosts static files as a website | Gives you a full virtual server | Runs code without a server |
| **Best for** | Portfolio, landing pages | Full web apps, databases | APIs, microservices, automation |
| **Server management** | None | You manage everything | None |
| **Scalability** | Automatic | Manual (you add more instances) | Automatic |
| **Cost** | Pay per storage + requests | Pay per hour (even when idle) | Pay per execution only |
| **Complexity** | Very Easy | Medium | Easy |
| **Free tier** | 5 GB, 20K requests | 750 hrs/month (12 months) | 1M requests/month (ALWAYS free) |
| **Custom domain** | Yes (with Route 53) | Yes (with Elastic IP) | Yes (with custom domain in API GW) |
| **SSL/HTTPS** | Via CloudFront | You configure manually | Built-in |
| **Real-life analogy** | Digital notice board | Renting a computer | Vending machine |

### When to Use What?

```
Need a simple portfolio or documentation site?
  --> Use S3 Static Hosting

Need to run a database, install custom software, or need full control?
  --> Use EC2

Need to build an API, process events, or run code on-demand?
  --> Use Lambda + API Gateway

Need all three?
  --> Use S3 for frontend + API Gateway + Lambda for backend + EC2 for database
```

---

## 8. Common Mistakes to Avoid

### S3 Mistakes
| Mistake | Solution |
|---|---|
| Bucket name not unique | Add your name and random numbers to the bucket name |
| Website not loading | Check if you unblocked public access AND added the bucket policy |
| 403 Forbidden error | The bucket policy might have a typo in the bucket name |
| Using wrong URL | Use the "Static website hosting" URL, not the S3 object URL |

### EC2 Mistakes
| Mistake | Solution |
|---|---|
| Can't SSH | Check Security Group has port 22 open |
| Lost .pem key file | You cannot recover it. Terminate instance and create a new one |
| Website not loading | Check Security Group has port 80 open |
| "Permission denied" on SSH | Run `chmod 400 your-key.pem` |
| Getting charged after free tier | Always TERMINATE (not stop) instances when done |
| Wrong username in SSH | Use `ec2-user` for Amazon Linux, `ubuntu` for Ubuntu |

### Lambda + API Gateway Mistakes
| Mistake | Solution |
|---|---|
| Lambda timeout | Increase timeout in Configuration > General (default is 3 seconds) |
| CORS error in browser | Add `Access-Control-Allow-Origin: *` in response headers |
| 502 Bad Gateway | Check Lambda function has correct return format with statusCode and body |
| Can't find API URL | Go to API Gateway > APIs > Your API > Stages |

---

## 9. Useful Resources

### Official AWS Documentation
- [S3 Static Hosting Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [EC2 Getting Started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
- [Lambda Getting Started](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html)
- [API Gateway Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)

### Free Learning Resources
- [AWS Free Tier Details](https://aws.amazon.com/free/)
- [AWS Skill Builder](https://skillbuilder.aws/) - Free courses from AWS
- [AWS Well-Architected Labs](https://wellarchitectedlabs.com/) - Hands-on labs

### YouTube Channels for AWS Learning
- AWS Official Channel
- TechWorld with Nana
- freeCodeCamp
- Abhishek Veeramalla (Hindi)

---

## Quick Reference Card

```
============================================
         AWS QUICK REFERENCE CARD
============================================

S3 STATIC WEBSITE:
  1. Create Bucket (unique name)
  2. Unblock public access
  3. Upload HTML files
  4. Enable static hosting
  5. Add bucket policy (public read)
  6. Access via S3 website URL

EC2 + NGINX:
  1. Launch t2.micro (free tier)
  2. Create/download key pair (.pem)
  3. Security group: open port 22, 80
  4. SSH: ssh -i key.pem ec2-user@IP
  5. sudo yum install nginx -y
  6. sudo systemctl start nginx
  7. Edit /usr/share/nginx/html/index.html

LAMBDA + API GATEWAY:
  1. Create Lambda function (Python)
  2. Write handler code
  3. Test with test event
  4. Create HTTP API in API Gateway
  5. Add Lambda integration
  6. Create POST route
  7. Get invoke URL and test with curl

============================================
```

---

**Made with care for engineering students. Happy Cloud Computing!**

**Author:** Sarthak Pawar  
**Date:** April 2026  
**License:** MIT - Feel free to share and use!
