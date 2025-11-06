<img width="635" height="289" alt="Screenshot 2025-11-06 144821" src="https://github.com/user-attachments/assets/9212e3c2-30ab-4532-be5e-ca3b643e2e8e" />
The Above task was achieved Using vagrant VMs
<img width="1059" height="1005" alt="Screenshot 2025-02-19 103918" src="https://github.com/user-attachments/assets/d7979bff-e7bf-48c5-9bdf-ff15bdca0e6d" />
i define a Vagrantfile to Launch 3 Dabian VMs, One as Master, followed by 2 server Nodes.
stage2 VMs Launching & Configuring Ansible on the Matser Node
a. Installing Ansible on The MasterVM
after laucnhing the 3 Virtual VMs, we ssh into the master VM where Ansible will be configured as we know asnsible is an agentless configuartion mgt tool unlike puppet and chef. 
<img width="956" height="367" alt="Screenshot 2025-02-19 105213" src="https://github.com/user-attachments/assets/36a59d41-e0ca-43fa-9279-bc01607bbcfc" />
Update the pakage manager (sudo apt update && sudo apt Upgrade) the first command to run after launching a VM
after the update is complete, define a bash script to install ansible on the master VM
<img width="871" height="493" alt="Screenshot 2025-02-19 105836" src="https://github.com/user-attachments/assets/bda888ab-f1ff-44ac-87ef-05e2b03b919d" />
Ansible 2.14.18 Installed along with Python because Ansible is written in Python, and it uses Python modules to execute tasks (especially on remote machines).

b. Ansible Configuration on the Master VM
<img width="338" height="166" alt="Screenshot 2025-02-19 110302" src="https://github.com/user-attachments/assets/43c73065-5bcb-44c6-bed3-dc2cee37aba8" />
we switch to root user and root password 

<img width="749" height="823" alt="Screenshot 2025-02-19 110518" src="https://github.com/user-attachments/assets/58c44bad-12c8-4328-bd1c-9e5eb403f12e" />
using vi or nano, go into  /etc/ssh/sshd_config  file and set PermitRoot Login, PubkeyAuthentication, & PasswordAuthentication all to yes.​
Note 'repeat this same steps on the 2Server Nodes'

Stage 3. SSH Handshake
Ansible is agentless, meaning it does not install any software or daemon on the remote servers, instead it uses SSH(Secure Shell)to connect from the Ansible Master Node → to the slave Servers. 
<img width="650" height="493" alt="Screenshot 2025-02-19 110636" src="https://github.com/user-attachments/assets/e333cece-10c2-41ad-8970-dc95ae21aabf" />
Generate ssh keys on the master node(ssh-keygen)
the above command will generate ssh key pairs, one as private key, and the other as publick keys.
