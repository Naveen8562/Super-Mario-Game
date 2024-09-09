# Super-Mario-Game
90's kids biggest fantasy  game 
P
r
o
j
e
c
t
:
🎮
Super
 
 
M
a
r
i
o
 
B
r
o
s
🍄
🐢
Project Workflow
Step 1 → Login and basics setup

Step 2 → Setup Docker ,Terraform ,aws cli , and Kubectl

Step 3 → IAM Role for EC2

Step 4 →Attach IAM role with your EC2

Step 5 → Building Infrastructure Using terraform

Step 6 → Creation of deployment and service for EKS

Step 1 → Login and basics setup
Click on launch Instance

image

Connect to EC2-Instance

image

Step 2 → Setup Tools
sudo apt update -y
Setup Docker:

sudo apt install docker.io
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker
docker --version
Setup Terraform:

sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update
sudo apt-get install terraform
terraform --version

Setup AWS CLI:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip 
unzip awscliv2.zip
sudo ./aws/install
aws --version

Install kubectl
Download the latest release with the command:

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
Validate the binary

 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
Validate the kubectl binary against the checksum file:

echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
Install kubectl:

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
Note: If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:

chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
kubectl version --client
Step 3 → IAM Role for EC2
create role:

image

image

Step 4 →Attach IAM role with your EC2 
go to EC2 click on actions → security → modify IAM role option

administrator access
eks
image

image

Step 5 → Building Infrastructure Using terraform
Install GIT

sudo apt install git -y
git clone https://github.com/abhipraydhoble/Project-Super-Mario.git
cd Project-Super-Mario
cd EKS-TF
vim backend.tf
image

Create Infra:

terraform init
terraform validate
terraform plan
terraform apply --auto-approve
aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
Step 6 → Creation of deployment and service for EKS
change the directory where deployment and service files are stored use the command →

cd ..
create the deployment

kubectl apply -f deployment.yaml
Now create the service

kubectl apply -f service.yaml
kubectl get all
kubectl get svc mario-service
copy the load balancer ingress and paste it on browser and your game is running

image

Final Output: Enjoy The Game 🎮

image

Delete Infra

 terraform destroy -auto-approve
