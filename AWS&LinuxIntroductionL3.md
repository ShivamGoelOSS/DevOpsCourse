## AWS Regions - The Global Layer
- An AWS region is a geographically isolated area that contains multiple Availability Zones (AZs). Each region is designed to be independent providing data sovereignty, fault tolerance, and low latency.
- Example Regions: 
	- Region Name: US East (N. Virginia) 
	- Code: us-east-1
	- Location: North America
- Each region has its own set of resources, like EC2 instances, S3 buckets, and RDS databases.
## Availability Zones (AZ)
- Each region has multiple availability zones (usually 2-6).
- An AZ is a physically separate datacenter or a group of datacenters connected via low latency links.
- Example: 
	- Region: ap-south-1
		- ap-south-1a
		- ap-south-1b
		- ap-south-1c
## Virtual Private Cloud (VPC)
- Inside each region, you create a VPC - an isolated virtual network for your AWS resources. You can create multiple VPCs in a region.
- A VPC lets you define IP address ranges (CIDR blocks), Subnets, Route tables, Internet Gateways, Security Groups, NACLs.
# Subnets in AWS
- A subnet is a smaller network segment inside the VPC.
- Each subnet belongs to exactly one Availability Zone.
- Subnets divide the VPC into logical groups i.e. public vs private.
- One can attach routing rules to control internet access.
- Subnet best practices to be implemented for real projects:
	- Always use multiple AZs for redundancy.
	- Divide subnets into tiers i.e. public, private or isolated.
	- Use NAT Gateways for private subnet internet access.
	- Reserve enough CIDR space for scaling.
	- Tag subnets clearly (Env=Prod, Tier=Public)
	- Use Route Tables and Security Groups to isolate traffic.
## AWS Fields For Creating EC2 Instances
- **Name and Tags:**
	- **Name:** A **tag** where key = Name and value = whatever you choose. It helps you to identify the instance later. Optional but strongly recommended.
	- **Additional Tags:** One can add other key/value tags (for example, Environment = Production, Role = WebServer, etc.) These help with organization, cost-allocation, automation.
- **Application and OS Images (AMI):**  
	- AMI is the Amazon Machine Image that you choose. This contains the OS (e.g. Amazon Linux, Ubuntu, Windows) + possibly applications or configurations.
	- If you are in the free tier, you will want to select an AMI marked as free tier eligible.
	- There are categories: **quick start** OS images, **Marketplace** images (paid or free), **community** shared AMIs.
- **Instance Type:** 
	- It determines the hardware configuration: number of vCPUs, amount of RAM, network performance, etc. Example, t3.micro, m5.large etc.
	- You choose the type based on your workload (CPU bound vs memory bound vs general purpose).
	- Free Tier often restricts to small instance types like t2.micro or t3.micro depending on date/account.
- **Key Pair (Login):** 
	- You can choose an existing key pair or create a new one. This is especially for SSH login (Linux) or RDP (Windows).
	- If you proceed without a key pair, not recommended for production, you may have no way to connect securely.
- **Network Settings:** 
	- This section covers how your instance fits into your network (VPC, subnet, security group, public IP, etc.)
	- **VPC/Subnet:** Choose which VPC and subnet will the instance would be launched into.
	- **Auto-Assign Public IP:** Whether the instance gets a public IPV4 address at launch (makes it reachable from the internet). Default differs for default vs non default subnet.
	- **Security Group(s):** Virtual firewall rules for inbound/outbound traffic to/from the instance.
	- **Network Interfaces/Secondary Interfaces:** One may optionally attach additional network interfaces (advanced).
	- **Subnet Type:** Can be public or private which will determine accessibility and routing.
- **Configure Storage:** 
	- **Root volume + additional volumes:** The AMI defines a base/root volume; you can add more (EBS volumes) or use instance store volumes depending on instance types.
	- **Volume Type:** For EBS you might choose types like gp3, gp2, io1, io2, st1, etc. These differ in performance, cost, IOPS.
	- **Size (GiB):** You specify the size of each volume.
	- **IOPS/Throughput:** For certain volume types (io1, io2, gp3) you may need to specify IOPS (for high performance) and throughput.
	- **Delete on Termination:** Whether the volume (especially root) is deleted when the instance is terminated. Helps avoid orphan volumes/cost.
	- **Encryption:** Whether the volume is encrypted; if yes, which KMS key to use.
	- **Device Name:** Which device the volume would appear as inside the OS (e.g. /dev/xvda, /dev/sdb).
## Advanced Details
These are optional fields but often very important - especially for production deployments. According to the AWS docs, this section contains many parameters. Some of the key fields include:
- **IAM Instance Profile:** The IAM role that would be associated with the instance. Grants permissions to the instance (for example, to read/write to S3, access other AWS services) via the role.
- **Shutdown Behavior:** Choose whether when you shut down the instance from within the OS, the instance would stop or terminate.
- **Enable Termination Protection:**  Prevents accidental termination of the instance by users via console/CLI; one must disable it before termination.
- **Monitoring (detailed CloudWatch monitoring):** By default, EC2 sends metrics to CloudWatch every 5 minutes; you can enable detailed monitoring for 1-minute intervals (incurs cost).
- **Placement Group:** If you want your instance to be in a specific placement group (clustered/hpc/partition) for network performance or fault isolation.
- **Tenancy:** Default shared hardware or dedicated host/dedicated instance. You might choose "Dedicated" if you need hardware isolation.
- **User Data:** A script or cloud-init content that runs at launch to configure the instance (install packages, bootstrap, etc).
- **Elastic GPU/ GPU & FGPA Options:** If supported, you may choose GPU/accelerated hardware.
- **Network Performance Optimization:** Options such as enhanced networking (ENA), SR IOV support etc.
- **Boot Mode:** UEFI vs legacy BIOS etc (for some OS/hardware combinations).
- **Metadata options / IAM instance metadata service version & restrictions**: You can configure the version and use of Instance Metadata Service (IMDS) to improve security.
- **License Options:** For certain OS or software you may specify license types.
- **Tag Specifications At Launch:** Tags for the instance, volumes, network interfaces etc.
# Linux Fundamentals
### 1. What is Linux?
- Linux is an open-source operating system.
- Used in servers, cloud platforms, DevOps, and automation. 
- **Kernel**:
    - Controls CPU, memory, hardware, file system, processes.
    - Acts as the “brain” of the operating system.
- **Shell**:
    - Command-line interface to interact with the system.
    - Examples: `bash`, `sh`, `zsh`, `fish`.
### 2. Why Learn Shell Commands?
- Faster than GUI for many tasks.
- Used for automation and scripting. 
- Important for DevOps, debugging, and system navigation.
### 3. Basic Linux Commands
- `pwd` → Show current directory path.
- `cd` → Change directory.
- `mkdir` → Create a directory.
- `rmdir` → Remove an empty directory.
- `touch` → Create an empty file or update timestamp.
- `cat` → View file content.
- `echo` → Print or write text into a file.
- `history` → Show list of previously used commands.

**Lab Task:**
- Create a folder named `starting_point`.
- Go inside it.
- Create a file `secret_lair.txt`.
- Use `pwd` to show full path.
- Use `history` to check past commands.
### 4. File Management Commands
- `ls` → List files and folders (`ls -l`, `ls -a`, etc.).
- `cp` → Copy files or directories.
- `mv` → Move or rename files or directories.
- `rm` → Delete files or folders (`rm -r` for folders).
- `find` → Search for files or directories.
- `du` → Show folder size usage.
- `df` → Show total and free disk space.

**Lab Task:**
- Remove a directory if it exists.
- Delete a file named `delete.txt`.
- Find all `.txt` files in `/home/user`.
- Check size of `/var/log` using `du`.
### 5. Process Management Commands
- **Process** = a running program.
- `ps` → Show running processes.
- `top` → Real-time process and system monitor.
- `htop` → Improved version of `top` (if installed).
- `kill` → Stop a process using process ID (PID).
- `jobs` → Show background tasks.
- `bg`, `fg` → Run tasks in background or bring to foreground.

**Lab Task:**
- List all running processes.
- Find PID of `sshd`.
- Run `sleep 60 &` in background.
- Bring it to foreground using `fg`.
- Kill a process using its PID.
### 6. Permissions and Ownership
- `chmod` → Change file permissions.
- `chown` → Change file owner.
- `chgrp` → Change file group.

**Advanced Lab Task:**
- Open hidden directory `secret_lair`.
- Count subdirectories.
- Find the one with restricted permissions.
- Change its ownership.
- Save all answers in `/home/user/answer.txt`.
