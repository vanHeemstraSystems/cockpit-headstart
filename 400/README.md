# 400 - Add Container Support to Cockpit

Based on "How to add container support to red hat cockpit" at https://thenewstack.io/how-to-add-container-support-to-red-hat-cockpit/

## 100 - What You’ll Need

The only things you’ll need to add container support to Cockpit are:

- A running instance of Cockpit (either on CentOS or RHEL).
- A user with sudo privileges.

That’s it. Let’s make some magic. I’ll demonstrate on a freshly updated instance of CentOS 8.

## 200 - Enabling Cockpit

Prior to CentOS 8, you had to install Cockpit. With CentOS 8, on the other hand, it’s installed out of the box. Even though the software is installed, it’s not enabled. So the first thing to be done is to enable Cockpit.

Log into your CentOS or RHEL server. If the server has a desktop environment, open a terminal window. From the terminal, issue the command:
```
sudo systemctl enable --now cockpit.socket
```

When prompted, type your sudo password and hit Enter. After that command completes, Cockpit is enabled and ready to go.

## 300 - Accessing Cockpit

Before we continue on, let’s make sure you can access Cockpit. Point a web browser to: https://SERVER_IP:9090 (where SERVER_IP is the IP address of the hosting server). You should be greeted by the Cockpit login (Figure 1).
