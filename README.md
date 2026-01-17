# SSH_remote_server

Below are the steps to connect to an AWS EC2 instance using SSH

# 1 - Enable Public IPv4 address
# 2 - Add a Security Group
# 3 - Enable inbound rules:
- SSH connection through the 22/TCP port
# 4 - Enable Outbound rules:
- All traffic from anyone "0.0.0.0/0"
# 5 - Make sure NACL allows:
- Inbound: Port 22
- Outbound: All traffic
# 6 - During the creation of the EC2 instance, an SSH key pair was generated in "mykey.pem" format file, and this is called a private key
- From the SSH client, we run these commands:
  $ chmod 400 mykey.pem
  $ ssh -i "mykey.pem" username@IPv4_public
- Note: the username depends on the OS
