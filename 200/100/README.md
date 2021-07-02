# 100 - Installing and Enabling Cockpit on Red Hat Enterprise Linux

Cockpit is included in Red Hat Enterprise Linux 7 and later.

On RHEL 7, enable the Extras repository.
sudo subscription-manager repos --enable rhel-7-server-extras-rpms
RHEL 8 does not need any non-default repositories.

1. Install cockpit:
```
sudo yum install cockpit
```

2. Enable cockpit:
```
sudo systemctl enable --now cockpit.socket
```

3. On RHEL 7, or if you use non-default zones on RHEL 8, open the firewall:
```
sudo firewall-cmd --add-service=cockpit
sudo firewall-cmd --add-service=cockpit --permanent
```
