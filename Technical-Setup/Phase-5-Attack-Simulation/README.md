## What We're Learning

In this phase, we will learn how a phishing attack is performed from start to finish. We'll use **GoPhish** to create a fake login page, send a deceptive email, and track the victim's interaction. We'll also use **Wireshark** to capture the network traffic during the attack. This hands-on experience will give you a complete picture of the attack's lifecycle and will be the foundation for our detection system.


## Tools Needed

- Your **Kali Linux VM** (with GoPhish and Wireshark running).
- Your **Windows Server 2022 VM** (with the `victim` email account).


## Step-by-Step Process

### **Step 1: Start GoPhish and Prepare to Capture**

1. **Start GoPhish:** Open a terminal on your Kali VM and run GoPhish by typing `sudo ./gophish`. Keep this terminal window open.
2. **Start Wireshark:** Open Wireshark on your Kali VM and start a capture on your internal network interface (`eth0` or `enp0s3`).

### **Step 2: Create a Landing Page in GoPhish**

A **landing page** is the fake website the victim is directed to after clicking a phishing link.

1. In your web browser, navigate to the GoPhish admin panel (`https://127.0.0.1:3333`).
2. Log in with your credentials.
3. In the left-hand menu, click on **"Landing Pages"**.
4. Click the **`New Page`** button.
5. Give your page a name like "Fake Google Login."
6. Check the box that says **"Capture Submitted Data"**. This is the most important step; it tells GoPhish to save the username and password the victim enters.
7. Check the box that says **"Capture Passwords"**.
8. You can either import a real login page (e.g., from Google's sign-in page) or just use the simple default template. For this project, a simple template is fine.
9. Click **`Save Page`**.

### **Step 3: Create a Phishing Email in GoPhish**

1. In the GoPhish admin panel, click on **"Email Templates"**.
2. Click the **`New Template`** button.
3. Give it a name like "Important Account Alert."
4. In the body of the email, write a simple message that creates a sense of urgency, like "Your account has been suspended. Click here to verify your account."
5. Now, we'll insert the phishing link. In the email editor, use the `{{.URL}}` placeholder. This is a special tag that GoPhish replaces with your phishing link when it sends the email.
`Click here to verify: {{.URL}}`
6. Click **`Save Template`**.

### **Step 4: Create a Phishing Campaign**

A **campaign** combines all the pieces: the email, the landing page, and the list of targets.

1. In the GoPhish admin panel, click on **"Campaigns"**.
2. Click the **`New Campaign`** button.
3. Give the campaign a name like "Sber Phishing Test."
4. Choose the email template you just created.
5. Choose the landing page you just created.
6. Now, we'll set up the email server to send the email. Under "Sending Profile," choose **`New Profile`**.
    - Give it a name like "Sber Mail Server."
    - Set the **Host** to the IP address of your Windows Server 2022 VM (e.g., `192.168.1.5`).
    - Set the **Username** and **Password** to the credentials for your `attacker@sber.local` email account.
7. Under "Targets," add your `victim@sber.local` email address.
8. Click **`Launch Campaign`**.

### **Step 5: Execute the Attack**

1. On your **Windows Server 2022 VM**, open your email client (like Thunderbird).
2. Check the `victim@sber.local` inbox. You should see the phishing email.
3. Click the link in the email. It will take you to the fake landing page you created.
4. Enter some fake credentials (e.g., `victim` for username and `Phished!` for password) and click "Submit."

### **Step 6: Stop the Capture and Analyze**

1. Go back to your **Kali Linux VM** and stop the Wireshark capture by clicking the red square button.
2. Go back to the GoPhish campaign dashboard. You'll see the status change from "Emails Sent" to "Clicked Link" and "Submitted Data." Click on the campaign name to see the captured credentials.

## Success Checkpoints

- You successfully created a landing page and an email template in GoPhish.
- The campaign launched and the email arrived in the victim's inbox.
- The victim was able to click the link and submit credentials.
- **GoPhish successfully captured the submitted credentials.** This is a critical checkpoint.
- **Wireshark successfully captured the network traffic** during the attack.

## Key Concepts Learned

- **Landing Page:** A fake web page designed to trick a victim into giving up their information.
- **Email Template:** The design of the deceptive email used in the attack.
- **Campaign:** The entire process of a phishing attack, from creating the email to launching it and tracking the results.
- **Credentials:** The username and password of a victim.

## Phase Summary

*You have successfully executed a full-fledged phishing attack in a controlled environment. You've seen firsthand how an attacker crafts a malicious campaign and what happens when a victim falls for it. This is a major milestone and provides all the data we need for the next phase.*
