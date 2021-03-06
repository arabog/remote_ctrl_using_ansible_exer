Prerequisites
Key pair - You should have an AWS EC2 key pair already created in your AWS Console, and downloaded to your local mahcine. We are assuming the key pair name is udacity.pem.

EC2 instance - An AWS EC2 Ubuntu instance mapped with the udacity.pem key-pair should be running in your AWS account. Don't forget to associate a tag, such as Project:udacity to the instance.

Inventory file - The inventory file containing the public IP address of your AWS 
EC2 Ubuntu VM must be present in your exercise directory. Refer to the Exercise: Inventory File, if the inventory file is not available. The contents should be like:

[all]
169.254.123.12

Note that if you are using Udacity provided AWS account, then the public IP of the EC2 instance will change at the beginning of each new session.


Instructions
Go to the Security group of your EC2 instance, and add an inbound rule to allow 
incoming TCP communication on port 3000 from all public IPs (0.0.0.0/0).

Create a new Playbook file named main-remote.yml with the following code:

Notice the reference to all here. That refers to the [all] we added to the top of the inventory file in the previous exercise.

Create a role for setup. Remember how to do that? Your folder structure should be named after the role and should contain a tasks folder and a files folder. Just in case you need a reminder, your folder structure should look like this:

.
├── main-remote.yml     # Playbook file. 
└── roles
 └── setup
     ├── files
     │   └── index.js
     └── tasks
         └── main.yml

Create a simple web server file in NodeJS - roles/setup/files/index.js containing the following content.

var http = require("http");
var server = http.createServer(function (req, res) {
res.writeHead(200);
res.end("Hello world!");
});
server.listen(3000);

Add a new task file - roles/setup/tasks/main.yml. This task file should contain instructions to:

update apt packages
upgrade packages
install dependencies, such as NodeJS and NPM
install pm2
create a ~/web directory
copy index test page from files/index.js to ~/web/index.js
Start the weeb server using the command pm2 start ~/web/index.js -f
Refer to the manual steps from this tutorial. As a hint, the file should start by updating and upgrading the packages in the Ubuntu server like this:

---
- name: "update apt packages."
  become: yes
  apt:
    update_cache: yes

- name: "upgrade packages"
  become: tyes
  apt:
    upgrade: yes

Now let's run the Playbook using your inventory file and udacity.pem file:
# Assuming the udacity.pem and inventory files are present in the current directory

sudo ansible-playbook main-remote.yml -i inventory --private-key udacity.pem

Accessing the EC2 host at its public IP:3000
in d browser