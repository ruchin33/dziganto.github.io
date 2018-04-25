---
published: false
title: From Zero to Spark Cluster in Under 10 Minutes
categories: [Amazon EMR, Apache Spark, Apache Zeppelin, Big Data]
---

![image](/assets/images/name.jpeg?raw=true){: .center-image }

## Objective
In this no frills post, you'll learn how to setup a big data cluster on Amazon EMR in less than ten minutes. 

## Prerequisites
1. You have an AWS account.
2. You have setup a [Key Pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html#create-a-key-pair)
2. You have `Chrome` or `Firefox`
3. You have basic familiarity with the command line.
4. You have basic familiarity with Python. (Optional) 

## Foxy Proxy Setup
1. In `Chrome` or `Firefox`, add the **FoxyProxy** extension.
2. Restart browser after installing FoxyProxy.
3. Open your favorite text editor and save [this code](https://github.com/dziganto/dziganto.github.io/blob/master/_scripts/foxyproxy-settings.xml) as **foxyproxy-settings.xml**. Keep track of where you save it.
4. In your browser, click on the `FoxyProxy icon` located at top right.
5. Scroll down and click `Options`.
6. Click `Import/Export` on left-hand side.
7. Click `Choose File`. 
8. Select `foxyproxy-settings.xml`. 
9. Click `Open`.
10. Congratulations, Foxy Proxy is now setup.

## EMR Cluster Setup
1. Login in to [AWS](https://aws.amazon.com/).
2. Navigate to `EMR` located under **Analytics**.

![EMR](/assets/images/EMR.png?raw=true){: .center-image }

3. Click the `Create cluster` button.

![Create EMR Cluster](/assets/images/EMR_create_cluster.png?raw=true){: .center-image }

4. You are now in **Step 1: Software and Steps**. Click `Go to advanced options`.
> Here you can name your cluster and select whichever S3 bucket you want to connect to.

![EMR Advanced Options](/assets/images/EMR_advanced_options.png?raw=true){: .center-image }

5. Click the big data tools you require. I'll select `Spark` and `Zeppelin` for this tutorial.

![EMR Software](/assets/images/EMR_select_software.png?raw=true){: .center-image }

6. Click `Next` at bottom right of screen.
7. In **Step 2: Hardware**, select the instance types, instance counts, on-demand or spot pricing, and auto-scaling options.
> For this tutorial we'll simply change the instance type to `m4.xlarge` and Core to 1 instance. 
>
> Everything else will remain as default.
>
> See following picture for details.

![EMR Software](/assets/images/EMR_instance_types.png?raw=true){: .center-image }

8. Click `Next` at bottom right of screen.
9. The next page is **Step 3: General Cluster Settings** Here you have the chance to rename your cluster, select S3 bucket, and add a bootstrap script - among other options. 
10. Click `Next` at bottom right of screen.
11. The next page is **Step 4: Security**. It is imperative that you select a predefined key pair. 
> Do NOT proceed without a key!
12. Click `Create cluster` at bottom right of screen.
> A new screen pops up that looks like this: 

![EMR Cluster Creation](/assets/images/EMR_cluster_creation.png?raw=true){: .center-image }

10. Your cluster is finished building when you see a status of **Waiting** in green. 
> Be patient as this will take 5+ minutes depending on which big data software you installed. It's not unusual for the build process to take 10-15 minutes or more. 
>
> Here's what a complete build looks like:

![EMR Cluster Running](/assets/images/EMR_cluster_running.png?raw=true){: .center-image }

11. Congratulations, you have a cluster running Spark!

## Amazon EMR Dashboard
1. Security group for Master (MyIP)
2. MyIP for SSH
3. SSH in

## Install Miniconda
1. `wget https://repo.continuum.io/miniconda/Miniconda-latest-Linux-x86_64.sh -O ~/anaconda.sh`
2. `bash ~/anaconda.sh -b -p $HOME/anaconda`
3. `echo -e '\nexport PATH=$HOME/anaconda/bin:$PATH' >> $HOME/.bashrc && source $HOME/.bashrc`

## Turn on FoxyProxy 	
1. Open the browser with FoxyProxy installed
2. Click FoxyProxy icon
3. Click ```Use proxies based on their pre-defined patterns and priorities```

## Amazon EMR Dashboard
1. On EMR dashboard, click ```Enable web connection```
2. Copy the command at the bottom 
3. Open new Terminal tab 
4. Paste command which opens and forwards port (note: it will look like it's not working but it is so leave it alone)
3. On EMR dashboard, click Zeppelin button

## Update Zeppelin for Anaconda
1. Top right, click button with green dot
2. In drop down, select ```Interpreters```
3. Search for **python**
4. Click ```Edit```
5. Change **zeppelin.python** from ```python``` to `/home/hadoop/anaconda/bin/python`
6. Select dropdown for Interpreters again
7. Search for spark
8. Click ```Edit```
9. Change **zeppelin.pyspark.python** from ```python``` to `/home/hadoop/anaconda/bin/python`