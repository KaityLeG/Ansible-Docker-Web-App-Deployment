# Ansible-Docker-Web-App-Deployment
![image](https://user-images.githubusercontent.com/41273957/223285658-e7120edc-eac2-4de0-9458-a035e8ec2514.png)
⭐ Deploying a web-page application that collects user info with Ansible and Docker ⭐
As a DevOps Engineer, my role in this project is to launch an EC2 instance for each PostgreSQL, Nodejs, and React docker container writing 3 different playbook groups for this project.
The infrastructure will be be comprised of 1 control node and 3 worker nodes using EC2s.
With PostgreSQL serving as the database to collect registration info, Nodejs as the the backend of the web-page and React controlling the frontend side of the web-page. Each component will serve inside three separate Docker containers on the three worker nodes EC2s dedicated to them.

How to successfully make this happen?
First understand that all of the processes will be controlled inside the control node with EC2 Full Access Role.
📍 Inside the control node EC2 will be:
•⚙ ansible config file
•⚙ ansible dynamic inventory file
•🗃 PostgreSQL, Nodejs, and React nodes files with separate Ansible YAML files that will install docker images and run Docker on each respective component.

The 3 worker nodes files containing PostgreSQL, Nodejs, React will be configured inside the control node as followed:

🖥 PostgreSQL:
• init.sql
•🐳 Dockerfile
• 📖 Configured Ansible playbook YAML file installing and running Docker
•Make sure volume is created with docker container to keep integrity of the database’s data.
•⚙ Set environmental variables such as passwords etc
•🔐 use ansible vault for protection
•Create PostgreSQL Container
•🚦 (Make sure this instance security group accepts traffic from port 5432, 5000 and SSH)

🖥 Nodejs:
• 📂 Server files (configure .env file based on PostgreSQL environmental variables)
•🐳 Dockerfile
• 📖 Configured Ansible playbook YAML file installing and running Docker
•Create the Nodejs container and publish on port 5000
•🚦 Make sure this instance security group accepts traffic from port 5000 and 22(SSH)

🖥 React:
• 📂 Client files (configure .env filed to connect React Node to Nodejs Node by plugging in public IP of Nodejs instance followed by its respective port 5000)
• 🐳 Dockerfile
• 📖 Configured Ansible playbook YAML file installing and running Docker
• Create React container and publish on port 3000
•🚦 (Make sure this instance security group traffic accepts ports 3000 and 80 from anywhere)

Now the control node has done all the work using ansible playbooks configuration. Here is a simple view of what the 3 worker nodes will complete and run according to the ansible playbooks.

✅ PostgreSQL:
docker
init.sql
Dockerfile
docker build
docker run

✅ Nodejs:
docker
server files
Dockerfile
docker build
docker run

✅ React:
docker
client files
Dockerfile
docker build
docker run

