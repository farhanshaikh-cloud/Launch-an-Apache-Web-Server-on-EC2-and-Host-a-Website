Here's a hands-on AWS task for you to practice launching an Apache web server on an EC2 instance and hosting a website.

# Task: Launch an Apache Web Server on EC2 and Host a Website

## Objective

Create an EC2 instance, install Apache, host a custom HTML website, and access it through a web browser.

---

## Requirements

### Infrastructure

* AWS Free Tier eligible instance
* Amazon Linux 2 or Red Hat Enterprise Linux EC2 instance
* Security Group allowing:

  * SSH (Port 22) from your IP
  * HTTP (Port 80) from Anywhere (0.0.0.0/0)

---

## Step 1: Launch EC2 Instance

Create an EC2 instance with:

| Setting        | Value                  |
| -------------- | ---------------------- |
| Name           | Apache-WebServer       |
| AMI            | Amazon Linux 2         |
| Instance Type  | t2.micro               |
| Key Pair       | Create or use existing |
| Security Group | Allow SSH and HTTP     |

---

## Step 2: Connect to EC2

### Linux/macOS

```bash
ssh -i apache-key.pem ec2-user@PUBLIC-IP
```

### Windows (PuTTY)

Connect using:

```
ec2-user
```

---

## Step 3: Update the Server

For Amazon Linux:

```bash
sudo yum update -y
```

For RHEL:

```bash
sudo dnf update -y
```

---

## Step 4: Install Apache

### Amazon Linux

```bash
sudo yum install httpd -y
```

### RHEL

```bash
sudo dnf install httpd -y
```

---

## Step 5: Start Apache Service

```bash
sudo systemctl start httpd
```

Enable service at boot:

```bash
sudo systemctl enable httpd
```

Verify status:

```bash
sudo systemctl status httpd
```

Expected:

```
active (running)
```

---

## Step 6: Create Website

Navigate to Apache document root:

```bash
cd /var/www/html
```

Create webpage:

```bash
sudo nano index.html
```

Paste:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Website</title>
</head>
<body>
    <h1>Welcome to My Apache Web Server</h1>
    <h2>Hosted on AWS EC2</h2>
    <p>Created by Farhan</p>
</body>
</html>
```

Save:

```
CTRL + X
Y
ENTER
```

---

## Step 7: Set Permissions

```bash
sudo chmod 644 /var/www/html/index.html
```

---

## Step 8: Test Website

Open browser:

```
http://PUBLIC-IP
```

Example:

```
http://54.123.45.67
```

You should see your webpage.

---

# Bonus Challenges

### Challenge 1

Replace the page with a professional company website:

```html
Header
About Us
Services
Contact Us
Footer
```

---

### Challenge 2

Add CSS styling.

Create:

```bash
sudo nano style.css
```

Add colors, fonts, and layouts.

---

### Challenge 3

Host a multi-page website.

Create:

```bash
about.html
services.html
contact.html
```

Link them using:

```html
<a href="about.html">About</a>
```

---

### Challenge 4

Upload a website from your local machine.

From your PC:

```bash
scp -i apache-key.pem index.html ec2-user@PUBLIC-IP:/tmp
```

Move file:

```bash
sudo mv /tmp/index.html /var/www/html/
```

---

## Validation Checklist

* [ ] EC2 launched successfully
* [ ] SSH connection works
* [ ] Apache installed
* [ ] Apache service running
* [ ] HTTP port 80 open
* [ ] Custom website created
* [ ] Website accessible through browser
* [ ] Apache starts automatically after reboot

### Expected URL

```
http://<EC2-Public-IP>
```

If you complete this task, I can give you a Level 2 challenge: **Host a dynamic PHP website with a MySQL database on EC2**.
