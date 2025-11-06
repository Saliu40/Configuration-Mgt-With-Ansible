<img width="635" height="289" alt="Screenshot 2025-11-06 144821" src="https://github.com/user-attachments/assets/9212e3c2-30ab-4532-be5e-ca3b643e2e8e" />
The Above task was achieved Using vagrant VMs
<img width="1059" height="1005" alt="Screenshot 2025-02-19 103918" src="https://github.com/user-attachments/assets/d7979bff-e7bf-48c5-9bdf-ff15bdca0e6d" />
i define a Vagrantfile to Launch 3 Dabian VMs, One as Master, followed by 2 server Nodes.
stage2 VMs Launching 
after laucnhing the 3 Virtual VMs, we ssh into the master VM where Ansible will be configured as we know asnsible is an agentless configuartion mgt tool unlike puppet and chef. 
<img width="956" height="367" alt="Screenshot 2025-02-19 105213" src="https://github.com/user-attachments/assets/36a59d41-e0ca-43fa-9279-bc01607bbcfc" />
Update the pakage manager (sudo apt update && sudo apt Upgrade) the first command to run after launching a VM
after the update is complete, define a bash script to install ansible on the master VM
