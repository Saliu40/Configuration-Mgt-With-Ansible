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

 <img width="1136" height="561" alt="Screenshot 2025-02-19 113048" src="https://github.com/user-attachments/assets/3b3ed34f-74d5-40f0-be02-32c69a7780f8" />
Copy the ssh Public key to Authorized_keys files of the 2slave/worker nodes, so as to enable ssh-connection(hand-shake)
You can choose to do it manually if you have access to the worker node, or You can Automate it.
after successfull copy, try ssh connection from the master node, to the slave node using the slave node public ip to be sure ure successfully connectected.

Stage4. Creating Ansible Inventory File
The inventory file is where we list the servers (hosts) that Ansible will manage.
Ansible needs to know the following:
Which machines to connect to
Their IP addresses or hostnames
Optional: the SSH username & key to use
Optional: groups (e.g., webservers, dbservers)
Think of it like the address book for your servers.
<img width="575" height="368" alt="Screenshot 2025-02-19 114312" src="https://github.com/user-attachments/assets/a6ace7ac-9720-4763-9d22-1e641a44d66d" />
get the public ip address of Ur two server/worker node, use them to define Ur inventory file on the master node/server
<img width="1186" height="705" alt="Screenshot 2025-02-19 113429" src="https://github.com/user-attachments/assets/722a5bec-62ce-435f-a4d2-fa618f1b188e" />

if all the stages listed above are well configured, You should be able to do Ansible ping to show successfull configurations
<img width="712" height="493" alt="Screenshot 2025-02-19 114440" src="https://github.com/user-attachments/assets/bb9a8e81-ad34-4c90-8c76-297eafe591fa" />
i ping both of my server nodes names Tomcat_server, and maven_server

Stage5. Creating Ansible Configuration File on our master VM
The Ansible Configuration File (usually named ansible.cfg) is used to define how Ansible behaves — it controls Ansible’s default settings, such as:
Where our inventory file is located
Whether SSH should ask for passwords
Default remote user
Logging behavior
Roles and playbook paths
Privilege escalation settings (sudo)
And many other operational defaults
<img width="780" height="186" alt="Screenshot 2025-02-19 120543" src="https://github.com/user-attachments/assets/9b8838c5-734a-499b-a64e-39b2b477fff3" />

<img width="701" height="371" alt="Screenshot 2025-02-19 120531" src="https://github.com/user-attachments/assets/ba758a0c-00ad-4ea1-b803-0c11e434aa27" />

touch a file (vi or nano ansible.cfg), define or paste the above codes and save it
after saving the file, run the below commands to enable ansible recorgnises it as the default .cfg file
 A screenshot of a computer
 <img width="791" height="343" alt="Screenshot 2025-02-19 120749" src="https://github.com/user-attachments/assets/94d9c5b1-15d7-459f-8732-cbdf79e8d1b1" />

Stage6 Defining Ansible playbook
An Ansible Playbook is a file where we define tasks that Ansible should perform on our woker/slave nodes using Yml language— such as installing software, configuring services, deploying applications, or managing system settings.
It is the heart of Ansible automation.

<img width="405" height="941" alt="Screenshot 2025-02-19 225413" src="https://github.com/user-attachments/assets/518cb66a-c16a-4c4f-b401-f7e5ea11fc7b" />
the above playbook name is Tomcat.yml
we define the playbook on the master node, instructing ansible to install tomcat on the Tomcat_server node.(thats one of our 2slave node)

<img width="367" height="974" alt="Screenshot 2025-02-20 114249" src="https://github.com/user-attachments/assets/67bf0810-a9ee-4b82-ac20-2ecae0de4f75" />
Tomcat was successfully installed on the tomcat worker/slave node automatedly.
<img width="347" height="564" alt="Screenshot 2025-02-19 224833" src="https://github.com/user-attachments/assets/be5e4d3c-a611-4dca-a0e7-bcfc61c224bf" />
to confirm, we ssh into the tomcat worker node to chack.

we define another playbook to Install Maven on our other worker/slave node
<img width="405" height="941" alt="Screenshot 2025-02-19 225413" src="https://github.com/user-attachments/assets/4d56b16a-1a5a-4fe8-9732-40528ee8b4a9" />
name of the playbook is Maven.yml 
define on the  Master Vm for Ansible to installed Maven on the server node2, the Maven server
<img width="367" height="974" alt="Screenshot 2025-02-20 114249" src="https://github.com/user-attachments/assets/47799264-fa46-48c3-82f1-86d19d7233c9" />
the playbook report shows it run successfully.

<img width="363" height="296" alt="Screenshot 2025-02-20 114256" src="https://github.com/user-attachments/assets/68b30a7b-ef88-4621-971b-0d88b877b487" />

we ssh into worker node2 the Maven_server, and there it is.
with this Ansible Configuration, throught the master VM, we can controll all the worker/slave nodes to which ever direction we want. all it takes is just to get the right modules.
