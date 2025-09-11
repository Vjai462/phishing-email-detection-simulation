## What We're Learning

we are learning the fundamental concepts of how an **email server** operates by building our own. We are setting up a "digital post office" within our virtual lab, which is essential for creating a realistic environment for our phishing project. This phase teaches us about the roles of different email components and protocols, such as:

- **Email Server:** The core software that handles sending, receiving, and storing emails, acting as the central hub for all mail traffic.
- **Domain:** The name of our local email network (e.g., `sber.local`), which is like a company's address for email.
- **Email Accounts:** The individual digital mailboxes we create for our users, such as `victim@sber.local` and `attacker@sber.local`.


## Tools Needed

- **hMailServer** - Our digital post office software (free and user-friendly)
- **Windows Server 2022 VM** - The building where our post office will operate
- **Your web browser** - To download hMailServer


## Step-by-Step Process

## **Step 1: Prepare Your Windows Server 2022 VM**
### **Actions:**
1. **Start your Windows Server 2022 VM** in VirtualBox
2. **Wait for it to fully boot up** (you'll see the desktop)
3. **Open Internet Explorer or Edge browser**

### **🧠 Learning Note:**
Windows Server is like a more powerful version of regular Windows, designed to run services (like our email server) for multiple users.


Step 2: Download hMailServer

### **Actions:**
1. **Navigate to:** https://www.hmailserver.com/download
2. **Look for the latest version** (should be something like "hMailServer 5.6.8")
3. **Click the download link** for the full installer (not the upgrade version)
4. **Choose "Save file"** when prompted

### **Learning Note:**
hMailServer is like building a complete post office. It can receive mail from the outside, sort it, store it in individual mailboxes, and let people check their mail.


Step 3: Install hMailServer

### **Actions:**
1. **Double-click the downloaded hMailServer installer**
2. **Click "Next"** through the welcome screen
3. **Accept the license agreement** and click "Next"
4. **Choose installation location** (default is fine) and click "Next"
5. **Select components** - leave everything checked and click "Next"
6. **Choose "Use built-in database engine"** (this is simpler for learning)
7. **Create administrator password** - write this down! Use something like: `AdminPass123`
8. **Click "Install"** and wait for completion

### **Learning Note:**
The "built-in database" is like having a filing cabinet built into our post office to store all the mailboxes and messages, rather than using a separate storage building.


Step 4: First Launch and Configuration
### **Actions:**

1. **Look for hMailServer Administrator** icon on desktop or Start menu
2. **Double-click to launch hMailServer Administrator**
3. **You'll see a connection dialog** - click "Connect" (it should connect to localhost automatically)
4. **Enter the administrator password** you created earlier
5. **Click OK**

### **Learning Note:**
The Administrator tool is like the post office manager's control panel - from here we can create mailboxes, set up rules, and manage our entire email system.


## **Step 5: Create Your Email Domain**

### **What's a Domain?**
Think of a domain like your company's address. Instead of @gmail.com or @yahoo.com, we'll create something like @ourcompany.local for our virtual company.

### **Actions:**
1. **In hMailServer Administrator, look for "Domains" in the left panel**
2. **Right-click on "Domains"** and select "New Domain"
3. **Enter domain name:** `ourcompany.local`
4. **Click "Save"**
5. **You should see your domain appear in the list**

### **Learning Note:**
We use ".local" because this is only for our internal network. In the real world, companies buy domains like "company.com" from domain registrars.


## **Step 6: Create Email Accounts (Our First Mailboxes)**

### **We'll create 3 accounts:**
- [**admin@ourcompany.local**](mailto:admin@ourcompany.local) - The administrator
- [**victim@ourcompany.local**](mailto:victim@ourcompany.local) - Our phishing target
- [**attacker@ourcompany.local**](mailto:attacker@ourcompany.local) - Our simulated hacker

### **Actions for First Account:**
1. **Expand "ourcompany.local" in the left panel**
2. **Right-click on "Accounts"** and select "New Account"
3. **Enter Address:** `admin@ourcompany.local`
4. **Enter Password:** `AdminEmail123` (write this down!)
5. **Set Maximum size:** 100 MB (default is fine)
6. **Click "Save"**

   ### **Repeat for other accounts:**
- [**victim@ourcompany.local**](mailto:victim@ourcompany.local) with password: `VictimPass123`
- [**attacker@ourcompany.local**](mailto:attacker@ourcompany.local) with password: `AttackerPass123`

### **Learning Note:**
These accounts are like individual mailboxes in our post office. Each person gets their own secure mailbox that only they can access with their password.


✅ Success Checkpoints

### **Test Steps:**
1. **In hMailServer Administrator, go to "Utilities" menu**
2. **Click "Send Test Message"**
3. **Fill in:**
    - From: `admin@ourcompany.local`
    - To: `victim@ourcompany.local`
    - Subject: `Test Email - Server Working!`
    - Message: `This is a test to confirm our email server is working correctly.`
4. **Click "Send**
   
### **Check if it worked:**
1. **Go to "Domains" → "ourcompany.local" → "Accounts" → "[victim@ourcompany.local](mailto:victim@ourcompany.local)"**
2. **Double-click the victim account**
3. **Look for "Messages" tab** - you should see 1 message!


🧠 Key Concepts Learned

- **Email Server:** The computer program that handles email delivery
- **Domain:** Like a company address (e.g., @mycompany.com)
- **Email Account:** Individual mailboxes for users
- **SMTP:** The language email servers use to talk to each other (like postal codes)
- **POP3/IMAP:** Ways to check your email (like different ways to access your mailbox)


## Problems Encountered

- **Problem:** Windows Server 2022 can't install .NET Framework 3.5 through Windows Features
- **Phase:** Phase 1
- **Difficulty:** Medium
- **Solution:** Use Server Manager "Add roles and features" or PowerShell Enable-WindowsOptionalFeature
- **Learning:** Legacy applications often need older frameworks installed as optional features


📝 Phase Summary
In Phase 1, we successfully built the foundation for our phishing simulation. We installed and configured an email server, hMailServer, on our Windows Server 2022 virtual machine. This acted as our "digital post office," allowing us to create and manage email accounts for our project, such as the victim@sber.local and attacker@sber.local mailboxes. By completing this phase, we established an essential, isolated email environment, which is the starting point for all our future activities. We also gained practical experience with server administration, domain management, and the core components of an email system.


# **Learning Note

### **Windows Server 2022 Behavior:**
- **Modern Windows Server** comes with .NET Framework 4.x pre-installed
- **Legacy .NET 2.0/3.5** needs to be added as an optional feature
- **hMailServer** was built for older .NET versions, so it needs the legacy framework

### **This is Normal:**
Many older applications require legacy frameworks. This is common in IT environments!
