#!/bin/bash
# Reference baseline for the Milestone 1 Linux lab (Amazon Linux EC2).
# Run from the ec2-user administrator account. Do not delete ec2-user or remove
# it from wheel; it is the instructor recovery path. No passwords are included.

# 1. Create the role groups.
sudo groupadd m1readers
sudo groupadd m1operators

# 2–4. Create the three local test accounts.
sudo useradd -m -G m1readers m1reader
sudo useradd -m -G m1readers,m1operators m1operator
sudo useradd -m m1retired

# 5–6. Create both folders and a sample Published file.
sudo mkdir -p /srv/courselab/published /srv/courselab/working
echo "Team notice" | sudo tee /srv/courselab/published/notice.txt

# 7–8. Give readers read/traverse access to Published.
sudo chown -R root:m1readers /srv/courselab/published
sudo chmod 2750 /srv/courselab/published
sudo chmod 640 /srv/courselab/published/notice.txt

# 9–10. Give operators access to create and modify files in Working.
sudo chown root:m1operators /srv/courselab/working
sudo chmod 2770 /srv/courselab/working

# 11. Disable the retired test account.
sudo usermod -L -e 1 -s /sbin/nologin m1retired

# Check the configuration. Run access tests separately as each test account.
ls -ld /srv/courselab/published /srv/courselab/working
id m1reader
id m1operator
sudo passwd -S m1retired
