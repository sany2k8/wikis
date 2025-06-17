## Step-by-Step Guide to Configure SSH and Connect to AWS EC2 Instance

### Prerequisites

- **AWS Account:** You need an active AWS account.
- **EC2 Instance:** An EC2 instance launched and running.
- **Key Pair:** A private key file (usually `.pem`) downloaded during instance creation.
- **SSH Client:** Terminal (macOS/Linux), Git Bash (Windows), or tools like PuTTY for Windows.
- **Security Group:** Inbound rule allowing SSH (port 22) from your IP address.

---

### 1. Launch or Prepare Your EC2 Instance

- Log in to the AWS Management Console.
- Navigate to EC2 and launch a new instance or select an existing one.
- During launch, create or select an existing SSH key pair and download the `.pem` file.
- Ensure the security group attached to the instance allows inbound SSH (port 22) from your IP.

---

### 2. Locate Your SSH Private Key File

- Find the `.pem` file you downloaded when creating your EC2 instance.
- Example: `my-key.pem`
- **Note:** If you lose this file, you cannot recover it. You must create a new key pair and instance.

---

### 3. Set Correct Permissions on the Key File

- Open your terminal and navigate to the directory containing your `.pem` file.
- Run:

```bash
chmod 400 my-key.pem
```

- This ensures only you can read the key, which is required for SSH to work.

---

### 4. Find Your EC2 Instance’s Public IP or DNS

- In the AWS Console, go to EC2 > Instances.
- Select your instance and copy the **Public IPv4 address** or **Public DNS**.

---

### 5. Connect to the EC2 Instance via SSH

#### On macOS/Linux or Windows (with Git Bash):

- Use the following command, replacing `my-key.pem`, `ec2-user`, and `your_public_ip` as appropriate:

```bash
ssh -i my-key.pem ec2-user@your_public_ip
```

- Common default usernames:
    - **Amazon Linux:** `ec2-user`
    - **Ubuntu:** `ubuntu`
    - **CentOS:** `centos`
    - **RHEL:** `ec2-user` or `root`
- Example:

```bash
ssh -i ~/Downloads/my-key.pem ubuntu@54.123.45.67
```

- The first time you connect, you may see a prompt:

```
Are you sure you want to continue connecting (yes/no)?
```

Type `yes` and press Enter.


#### On Windows (with PuTTY):

- Convert `.pem` to `.ppk` using PuTTYgen.
- Open PuTTY, enter the instance’s public IP, set the username, and load the `.ppk` file under SSH > Auth.

---

### 6. Troubleshooting Common Issues

- **Permission Denied:** Ensure your key file has `chmod 400` permissions.
- **Timeout:** Check that your security group allows inbound SSH (port 22) from your IP.
- **Wrong Username:** Use the correct default username for your instance’s OS.
- **Key Not Found:** If you lost your key, create a new instance with a new key pair.

---

### 7. (Optional) Generate a New SSH Key Pair Locally

- If you want to generate your own key pair and upload the public key to AWS:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/my-ec2-key
```

- Upload the public key (`my-ec2-key.pub`) to AWS EC2 > Key Pairs > Import Key Pair.

---

### Summary Table

| Step | Command / Action |
| :-- | :-- |
| Set key permissions | `chmod 400 my-key.pem` |
| Find public IP/DNS | AWS Console > EC2 > Instances |
| Connect via SSH | `ssh -i my-key.pem ec2-user@your_public_ip` |
| Windows (PuTTY) | Convert `.pem` to `.ppk`, use with PuTTY |
| Generate new key pair | `ssh-keygen -t rsa -b 2048 -f ~/.ssh/my-ec2-key` |
| Import public key | AWS Console > EC2 > Key Pairs > Import Key Pair |


---

## Understanding Public and Private Keys

### What Are Public and Private Keys?

- **Public and private keys** are a pair of cryptographic keys used in SSH (Secure Shell) authentication and other encryption technologies.
- The **public key** can be shared openly. It is used to encrypt data or verify a digital signature. Anyone can have a copy of your public key.
- The **private key** must be kept secret and secure. It is used to decrypt data encrypted with the public key or to create digital signatures.
- The two keys are mathematically linked: data encrypted with the public key can only be decrypted with the corresponding private key, and vice versa.


### How SSH Authentication Works

- When you connect to a server (like an AWS EC2 instance) using SSH, the server checks if your public key is authorized.
- Your SSH client uses your private key to prove your identity. The server verifies this against the public key it has stored.
- This method is more secure than password-based authentication because only someone with the private key can log in.


## Where Are the Keys Stored in AWS EC2?

### On Your Local Machine

- **Private Key:**
    - When you create or download an AWS EC2 key pair, you receive a `.pem` file containing your private key.
    - This private key is **never stored on AWS or the EC2 instance**. It is your responsibility to keep it safe and secure on your computer.
    - If you lose this private key, you cannot access your instance via SSH unless you add a new key pair.


### On the EC2 Instance

- **Public Key:**
    - The public key is stored on the EC2 instance, specifically in the `~/.ssh/authorized_keys` file for the user you log in as (e.g., `ec2-user` or `ubuntu`).
    - When you launch an EC2 instance and specify a key pair, AWS injects the public key into this file at boot time.
    - The private key is **not** present on the EC2 instance.


#### Table: Key Locations

| Key Type    | Stored On Your Computer  | Stored On EC2 Instance         |
| :---------- | :----------------------- | :----------------------------- |
| Public Key  | Optional (for reference) | Yes (`~/.ssh/authorized_keys`) |
| Private Key | Yes (`.pem` file)        | **No**                         |

## Summary

- The **public key** is stored on the AWS EC2 instance to allow authentication.
- The **private key** is only on your computer; it is never uploaded to AWS or the instance.
- Keep your private key secure—anyone with it can access your instance.

This key pair system ensures secure, passwordless access to your AWS EC2 instances using SSH.


---

By following these steps, you can securely configure SSH and connect to your AWS EC2 instance from any supported operating system.

### References

- https://www.pump.co/guides/ssh-aws-ec2-instance
- https://mundobytes.com/en/connect-to-aws-ssh-instance/\&rut=21953e6c236c1a2f23a5ddcd77d5eb844b998f2383365764695af0e17cfc3e9f/
- https://dev.to/solardeath/ssh-into-your-ec2-instance-a-step-by-step-guide-e4c
- https://www.emtec.com/kb/en/2004/create-public-private-keys-for-aws-ec2
- https://www.pulumi.com/ai/answers/8GTiwEMxcW8RK4fsxuD6R3/python-ssh-key-generation-for-ec2-access
- https://www.youtube.com/watch?v=XnW6C9Ypkkw
- https://awstip.com/how-to-connect-to-the-ec2-instance-with-ssh-client-94840d136b03?gi=6ac2a3077307
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-linux-inst-ssh.html
- https://stackoverflow.com/questions/6394762/how-do-i-set-up-ssh-access-for-an-amazon-ec2-instance
- https://goteleport.com/learn/ssh-into-ec2-instance/

