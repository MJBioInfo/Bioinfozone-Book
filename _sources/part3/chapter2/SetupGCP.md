
In this chapter we are going to see how we can set up Google cloud to do RNAseq Alignment using free $300 credits (We can setup Business account also for longer term)

Follwing are steps to setup GCP :

# Creating New VM instance ( Like setting NEW linux machine) :

First you need to have a Google account to start. If not signup for a google account which is free and login google account . 

then go to 
https://console.cloud.google.com/ 

to setup your cloud account.

click on start free trail 
select whether you are individual or business . we have selected individual 
finish cloud account by providing credit or debit card information (which is only used to verify your detail and not charged )

figures


Next you have to create new project . Give a name to project and within this project we start configuring our Ubuntu machine and storage.


# Virtual Machine (Ubuntu) setup 

After creating project click on project . you can see 3 horizontal bars Menu icon at left side click that , then select Compute Engine and select VM instance .

Then click on Create instance
Page will ask you to specify your needs for new machine .

Note: Select proper Region because different regions have different price per hour . we have choosen Europe region according to our need.

There are different VM are present in google cloud and More powerful machines have more price / hour . So it is advisable to configure your VM machines according to your need . 

Here for our STAR alignment we need minimum 32 GB RAM and more threads ( 10 )

Clcik change button under Boot disk to specify UBUNTU 18.04 OS 

We specified hard disk space as 500 GB

under API acess click Full access

Under firewall click Allow HTTP and HTTPS

Click create buttom and you are done.

Now successfully you have created VM instance (Ubuntu machine)

to connect to machine we click on SSH button . It will open SSH broser Terminal (similar to ubuntu terminal)

Now we can use this Machine for RNAseq analysis . 

Before proceeding we need to create a Bucket for storage to transfer files between Virtual Machine and your google cloud account.

