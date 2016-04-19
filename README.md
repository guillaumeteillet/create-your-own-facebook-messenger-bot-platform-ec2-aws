# Getting started with Facebook Messenger Platform on EC2 (AWS)
This walkthrough describes how to create your own bot with Facebook Messenger Platform in few easy steps and how to run it on your EC2 (Amazon Web Service).

### Prerequisites

- An AWS account
- A domain name (in this tutorial : yourdomainname.com)

### 1. Create an EC2 instance

First of all, you need to create an EC2 instance. On Amazon Web Service, select EC2 :

![AWS Panel](https://cloud.githubusercontent.com/assets/1462301/14611818/6c605b88-0594-11e6-8e10-86e8bc62791b.png)

In the left menu, choose "Instances" :

![Choose Instance](https://cloud.githubusercontent.com/assets/1462301/14611937/00c9737c-0595-11e6-86f5-7f8604b00d45.png)

On the Instance page, clic on "Launch Instance" on the top menu :

![Top Menu](https://cloud.githubusercontent.com/assets/1462301/14612021/5ee09dbe-0595-11e6-9b44-839bd08faa8d.png)

"Step 1: Choose an Amazon Machine Image (AMI)" : You should select "Ubuntu Server 14.04 LTS (HVM), SSD Volume Type - ami-f95ef58a" :

![Select Ubuntu](https://cloud.githubusercontent.com/assets/1462301/14612107/e0682ab4-0595-11e6-862f-3417b92efad9.png)

"Step 2: Choose an Instance Type" : Verify that the instance t2.micro  is selected and clic on "Review and launch"

![Review and Launch](https://cloud.githubusercontent.com/assets/1462301/14612294/a60656d8-0596-11e6-804b-81da57f9689d.png)

"Step 7: Review Instance Launch" : Clic on "Launch" (Right bottom of the page)

If you already used AWS, you already have a key pair so you can use it and for finish, clic on "Launch Instance" 

![Use Keypair](https://cloud.githubusercontent.com/assets/1462301/14612500/97472d9c-0597-11e6-9630-f4de9d139dc2.png)

If you never used AWS, you should create a new key pair : Enter the name of your key pair (can be what you want) and clic on "Download Key Pair" and for finish, clic on "Launch Instance"

![Create Keypair](https://cloud.githubusercontent.com/assets/1462301/14612584/28291816-0598-11e6-9f16-bcf17e36e714.png)

Now, you should have this page : Clic on "View Instances"  (Right bottom of the page)

![EC2OK](https://cloud.githubusercontent.com/assets/1462301/14612712/f2e36282-0598-11e6-9c45-d9b59cf3b759.png)

A new instance is launching : 

![EC2LAUNCHING](https://cloud.githubusercontent.com/assets/1462301/14612771/42503606-0599-11e6-9e2e-b86c049eca43.png)

After few minutes, when the EC2 instance is ready, you should see this : 

![EC2READY](https://cloud.githubusercontent.com/assets/1462301/14612823/94b4cdee-0599-11e6-8a80-aba0d38c2911.png)

If you clic on it, you will see all the details about the EC2 Instance.

![EC2DETAILS](https://cloud.githubusercontent.com/assets/1462301/14612929/074f2002-059a-11e6-8073-dacc0677347e.png)

### 2. Change your DNS

In this tutorial, you need your own domain name. Mine is [guillaumeteillet.fr](http://guillaumeteillet.fr)

For this step, we will use a new service of AWS called "Route 53" :

![ROUTE53](https://cloud.githubusercontent.com/assets/1462301/14613120/2876cb4e-059b-11e6-9f6f-24f18666e254.png)

In the left menu, select "Hosted zones" :

![HOSTEDZONE](https://cloud.githubusercontent.com/assets/1462301/14613152/57a3bef4-059b-11e6-9f35-23dfe176df70.png)

Then clic on "Create Hosted Zone" : 

![HOSTEDZONEBUTTON](https://cloud.githubusercontent.com/assets/1462301/14613253/da6afd3e-059b-11e6-9175-7f026e59cb6b.png)

Enter your domain name (mine is [guillaumeteillet.fr](http://guillaumeteillet.fr)) and then clic on "Create" :

![DOMAINNAMEHOSTEDZONE](https://cloud.githubusercontent.com/assets/1462301/14613416/a932d614-059c-11e6-80c6-51acc18c549a.png)

Route 53 has created two Record Set in your Hosted Zone : We will need the 4 DNS (red square on the picture)

![ROUTE53RECORDSET](https://cloud.githubusercontent.com/assets/1462301/14613523/11bfa950-059d-11e6-9569-27a0ac1f61db.png)

Now, change the DNS Name of your domain name (My registar is [OVH](http://ovh.com) so perhaps the procedure is a bit different) :

Before any change, the DNS name was : 

![BEFOREDNS](https://cloud.githubusercontent.com/assets/1462301/14614072/c1a58e0a-059f-11e6-83ea-98ddfaf7d46a.png)

The registar need some time to change the DNS of your domain name : 

![DURINGTHECHANGEDNS](https://cloud.githubusercontent.com/assets/1462301/14614142/06613cec-05a0-11e6-88c3-588cdbd54ed5.png)

After few minutes, the 4 DNS of your domain name should be active : 

![AFTERDNS](https://cloud.githubusercontent.com/assets/1462301/14614311/e6e0ead8-05a0-11e6-8a98-64b82d70d184.png)

Now, go back on AWS, choose EC2 and then choose "Instances" on the left menu. We need the public IP, mine is 54.171.135.46, copy this ip. 

![EC2DETAILSIP](https://cloud.githubusercontent.com/assets/1462301/14614532/e8896710-05a1-11e6-8c61-8d131198542f.png)

Now, go to "Route 53" :

![ROUTE53CHANGE](https://cloud.githubusercontent.com/assets/1462301/14614717/9b73e68e-05a2-11e6-9428-5f9298a15691.png)

Select "Hosted Zones" in the left menu, clic on your domain name : You will arrived on the list of the Record Set.

![MYDOMAINNAME](https://cloud.githubusercontent.com/assets/1462301/14614866/5ab6dff6-05a3-11e6-8072-113f37fab582.png)

Clic on "Create Record Set" : 

![RECORDSET](https://cloud.githubusercontent.com/assets/1462301/14614930/b0d714e6-05a3-11e6-9b72-fd9481523321.png)

We will now create two record set. First, keep the field name empty and in the field value, paste the public ip of your ec2 instance. For the type of the record set, choose A - IPV4 Address

![AIPV4](https://cloud.githubusercontent.com/assets/1462301/14644785/9818ee56-0653-11e6-9a2f-4048922c4bc9.png)

Next, in the field name, enter "www", in the field value, paste the public ip of your ec2 instance. For the type of the record set, choose A - IPV4 Address.

![AIPV4WWW](https://cloud.githubusercontent.com/assets/1462301/14645682/f08dd0f8-0656-11e6-97e1-a890b59aeaf8.png)

Now, you should wait few minutes. You can use this tool [WhatsmyDNS](https://www.whatsmydns.net/) to see if your domain name is now using the good ip address : Enter your domain name (mine is guillaumeteillet.fr) and clic on "Search". If the IP Address of your EC2 Instance appears, it means your domain name is now using the good ip address, you can continue this tutorial.

![TOOLIP](https://cloud.githubusercontent.com/assets/1462301/14646185/dac68916-0658-11e6-9688-b8bda5e452a7.png)

### 3. Connect to your EC2 Instance

On Amazon Web Service, select EC2, Instances (in the left menu), select your instance and clic on "Connect" (in the top menu).

![CONNECTEC2](https://cloud.githubusercontent.com/assets/1462301/14646829/615f68ce-065b-11e6-9d32-bcace60ce58e.png)

Copy the ssh command. Mine is "ssh -i "Guillaume.pem" ubuntu@ec2-54-171-135-46.eu-west-1.compute.amazonaws.com". Open a terminal, go to the folder that contains the key pair and paste the ssh command.

![TERMCONNECTION](https://cloud.githubusercontent.com/assets/1462301/14647960/475d5e04-0660-11e6-806f-62fc6b5754a3.png)

Now your are connected on your EC2 Instance. 

### 4. Get the code

Run this on your EC2 instance :

```bash
sudo su
apt-get update
apt-get install -y git
git clone https://github.com/guillaumeteillet/create-your-own-facebook-messenger-bot-platform-ec2-aws.git
cd create-your-own-facebook-messenger-bot-platform-ec2-aws
apt-get install -y npm
npm install
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
apt-get install -y nodejs
apt-get install -y nano
apt-get install -y apache2
cd /etc/apache2/sites-available
nano yourdomainname.com.conf
```

The text editor nano opens, copy and paste this :

```bash
<VirtualHost *:80>
	ServerName www.yourdomainname.com

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Where "www.yourdomainname.com" should be replace by your own domain name.

Save your file : Ctrl + X + S, then press y and enter

In the same directory, run this on your EC2 instance :

```bash
a2ensite yourdomainname.com.conf
```
You should have this return : 

```bash
Enabling site yourdomainname.com.
To activate the new configuration, you need to run:
  service apache2 reload
```

So now, you have to reload apache2. Just run this command : 

```bash
service apache2 reload
```
You should have this return : 

```bash
 * Reloading web server apache2                                                                                                       * 
```

### 5. HTTPS with [Let's encrypt](https://letsencrypt.org/getting-started/)

Run this on your EC2 instance :

```bash
cd
sudo su
git clone https://github.com/letsencrypt/letsencrypt
cd letsencrypt
./letsencrypt-auto
```

Facebook required a https webhook, so we will use let's encrypt to get our ssl certificate.
When ./letsencrypt-auto is ready (few minutes), you will see this : 

![LETSENCRYPT1](https://cloud.githubusercontent.com/assets/1462301/14651185/1e2aa5dc-066f-11e6-91f5-ffa202a929d9.png)

As you can see, my domain "www.guillaumeteillet.fr" is selected ([*]). You can selected/unselected domain with space bar, navigate with up and down. When the domain name for which you want a SSL certificate is selected, press Enter.

Let's encrypt ask your email address to notify you when the certificate expires. Enter a valid email and press Enter. 

Press Enter again when let's encrypt ask you if you read the Terms.



