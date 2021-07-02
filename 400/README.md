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

![image](https://user-images.githubusercontent.com/12828104/124254310-3c7e8a00-db29-11eb-8759-16b1e5921be7.png)

Figure 1: The Cockpit login.

Log in with the root user’s credentials, making sure to check the box for ***Reuse my password for privileged tasks***. Why? Because at the moment, Podman isn’t capable of running rootless containers, so you’ll need that heightened privilege to work with Podman.

However, we’ve not added Podman support yet. So let’s add it. Log out of Cockpit and head back to the terminal window.

## 400 - Adding Podman Support

In order to add Podman support, you’ll need to install another application. At the terminal window, issue the following command:
```
sudo dnf install cockpit-podman -y
```

Once that command completes, log back into Cockpit (with root’s credentials) and you should see ***Podman Containers*** listed in the left sidebar (Figure 2).

![image](https://user-images.githubusercontent.com/12828104/124254843-c75f8480-db29-11eb-8907-e834cfe473a6.png)

Figure 2: We’ve successfully added Podman support to Cockpit.

Click ***Podman Containers*** in the left navigation and you’ll see a warning that the service isn’t running (Figure 3).

![image](https://user-images.githubusercontent.com/12828104/124255052-068dd580-db2a-11eb-8c92-0b412e6e9081.png)

Figure 3: The Cockpit Podman service isn’t running.

Make sure the checkbox for ***Automatically start podman on boot*** is checked, and then click ***Start podman***.

You should now see the Podman Containers Cockpit dashboard (Figure 4).

![image](https://user-images.githubusercontent.com/12828104/124255345-59678d00-db2a-11eb-9d98-db3ace78dc9c.png)

Figure 4: The Podman Container dashboard.

Unless you’ve already used the podman command line, you won’t have any images or containers listed in the dashboard. Let’s fix that.

To download a new image, click ***Get new image***. In the resulting pop-up (Figure 5), type the name of the image you want to download and wait for the results.

![image](https://user-images.githubusercontent.com/12828104/124255753-d0048a80-db2a-11eb-9774-0da316851940.png)

Figure 5: Downloading a container image via Cockpit.

Once the results have appeared (Figure 6), select the image you want and click ***Download***.

![image](https://user-images.githubusercontent.com/12828104/124255957-09d59100-db2b-11eb-814a-d8589df03e3c.png)
Figure 6: Selecting the exact image you want to use.

There’s one caveat you’ll experience on CentOS. Unless you’re a subscriber to RHEL, you won’t be able to download images from the Red Hat repositories. That’s okay, because if you scroll down, you’ll find images from other sources.

After the image downloads, you’ll see it listed in the Dashboard. Click the run button (right-pointing arrow) associated with the image and you can then configure a container to be deployed in the resulting popup window (Figure 7).

![image](https://user-images.githubusercontent.com/12828104/124256203-54efa400-db2b-11eb-9cc2-d16a9accf8c5.png)

Figure 7: Configuring your container for deployment.

Your deployed container will now be listed in the Podman Dashboard (Figure 8).

![image](https://user-images.githubusercontent.com/12828104/124256408-8bc5ba00-db2b-11eb-816a-64c55c0a9241.png)

Figure 8: A running container listed in the Podman Cockpit Dashboard.

And that’s all there is to adding container support to the Cockpit web-based GUI. Although you might not work all of your container magic within the confines of this tool, it can make the management of your containers and images significantly easier.
