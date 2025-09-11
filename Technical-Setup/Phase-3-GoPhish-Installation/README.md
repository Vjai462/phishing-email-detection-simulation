## What We're Learning

In this phase, we'll install **GoPhish**, an open-source tool for phishing simulations. Think of GoPhish as a special toolbox that lets you create fake emails and websites for a phishing campaign. Cybersecurity professionals use tools like this to test how well a company's employees can spot a phishing attack. For our project, we will use it to create a realistic attack so we can analyze it later.


## Tools Needed

- Your **Kali Linux VM** (already set up).
- Your web browser.
- The terminal in Kali Linux.


## Step-by-Step Process

### **Step 1: Download GoPhish**

1. **Start your Kali Linux VM:** Power on your Kali Linux virtual machine in VirtualBox.
2. **Open the Terminal:** Once Kali has loaded, open a terminal window.
3. **Find the GoPhish download:** GoPhish is a simple program that doesn't need a complex installation. We just need to download it. Visit the official GoPhish GitHub page from your Kali Linux web browser. The URL is typically `https://github.com/gophish/gophish/releases`.
4. **Download the correct version:** Look for the latest release and find the file for **Linux 64-bit**. The name will look something like `gophish-v0.12.1-linux-64bit.zip`. Click the link to download the file.

### **Step 2: Unzip and Move the GoPhish Files**

1. **Go to your Downloads folder:** In the terminal, type `cd ~/Downloads` to move to the directory where the file was saved.
2. **Unzip the file:** GoPhish is downloaded as a compressed file. We need to uncompress it. Use the command `unzip gophish-v0.12.1-linux-64bit.zip`.
3. **Move the folder:** For better organization, we will move the GoPhish files to a more suitable location. Type `sudo mv gophish /opt/gophish`.
    - **`sudo`** grants us administrative privileges.
    - **`mv`** is the command to "move" files.
    - `/opt` is a standard directory for optional or third-party software
  
### **Step 3: Edit the GoPhish Configuration**

1. **Change directory:** Move into the GoPhish folder with `cd /opt/gophish`.
2. **Open the config file:** We need to edit a file named `config.json`. We'll use the Nano text editor. Type `sudo nano config.json`.
3. **Change the listening address:** Inside the file, you'll see a line that says `"listen_url": "127.0.0.1:3333"`. We need to change `127.0.0.1` to `0.0.0.0`. This tells GoPhish to listen for connections from any IP address on our network, not just the local computer. The line should now read `"listen_url": "0.0.0.0:3333"`.
4. **Save and exit:** Press `Ctrl + X`, then `Y`, and then `Enter` to save the changes and exit the file.

### **Step 4: Launch GoPhish for the First Time**

1. **Run the program:** In the terminal, with the GoPhish folder open, type `sudo ./gophish`.
    - The `./` part means we are running a program in the current folder.
2. **Get the URL:** GoPhish will now start. The terminal will show a message with the URL and default credentials to access the web interface. Look for a line that says "Please navigate to `https://127.0.0.1:3333`..."
3. **Access the web interface:** On your Kali Linux VM, open a web browser and navigate to the address shown. Ignore any security warnings about the certificate; it's just for our lab.
4. **Log in:** The default username is **`admin`**. Use the password from the `config.json` file. You will be prompted to change it. Change it and save it.


##  Success Checkpoints

- After Step 2, you should see the `gophish` folder in your `/opt` directory.
- After Step 3, the `config.json` file should show the changes you made.
- After Step 4, the terminal should show GoPhish is running, and you should be able to log in to the web interface.


## Key Concepts Learned

- **Phishing Simulation Toolkit:** A tool used by security professionals to create fake phishing campaigns for training and testing purposes.
- **GoPhish:** The specific open-source toolkit we are using.
- **`config.json`:** A file that stores the configuration settings for a program. Editing this lets us customize how the program works.
- **`sudo`:** A command that temporarily gives you administrative rights to run commands.
- **IP Addresses (127.0.0.1 vs 0.0.0.0):** `127.0.0.1` refers only to the local computer, while `0.0.0.0` means "all network interfaces," allowing other computers in our lab to connect.


## Phase Summary

In this phase, we've successfully installed GoPhish on our Kali Linux VM and configured it to work within our lab network. We now have a powerful tool to create and manage our phishing campaigns, which is the next major step in our project.*

We successfully:

- Downloaded the correct pre-compiled GoPhish binary for Linux.
- Unzipped the files and moved them to the `/opt/gophish` directory for organization.
- Edited the `config.json` file to allow GoPhish to be accessed by other machines in our virtual network.
- Started the GoPhish server from the command line.
- Resolved common errors, including conflicts with other web servers, and successfully accessed the GoPhish admin login page to set a new password.

This phase was a crucial step in preparing our lab for the actual phishing simulation.
