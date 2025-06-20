## Step-by-Step Guide: Set Up and Configure AWS CLI

### **1. Install the AWS CLI**

- **Windows:** Download the installer from the official AWS website, run the `.msi` installer, and follow the prompts.
- **macOS:**
    - Download the `.pkg` installer from AWS and run it, or
    - Install via Homebrew:

```bash
brew update
brew install awscli
```

- **Linux:** Download and run the official installer or use your package manager.

**Verify installation:**

```bash
aws --version
```

You should see the AWS CLI version printed in the terminal.

---

### **2. Create/Retrieve AWS Access Keys**

- Log in to the AWS Management Console with your IAM user account (not root).
- Navigate to **IAM** > **Users**.
- Select your user, then go to the **Security Credentials** tab.
- Click **Create Access Key**.
- Save the **Access Key ID** and **Secret Access Key** securely (download the `.csv` file if prompted).

---

### **3. Configure the AWS CLI**

Open your terminal and run:

```bash
aws configure
```

You will be prompted for:

- **AWS Access Key ID:** Enter the access key you just created.
- **AWS Secret Access Key:** Enter the secret key.
- **Default region name:** e.g., `us-east-1`, `eu-central-1` (choose the region you use most).
- **Default output format:** e.g., `json`, `text`, or `table` (usually `json`).

**Example:**

```
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: json
```


---

### **4. Verify Your Configuration**

Test your setup by running:

```bash
aws sts get-caller-identity
```

This should return your AWS account and user details, confirming your CLI is configured correctly.

---

### **5. Start Using the AWS CLI**

You can now run AWS CLI commands, such as:

```bash
aws s3 ls               # List S3 buckets
aws ec2 describe-instances  # Describe EC2 instances
```


---

### **Additional Notes**

- The configuration is stored in `~/.aws/credentials` and `~/.aws/config` files.
- You can manually edit these files for advanced configurations or multiple profiles.
- Ensure your computer's date and time are set correctly, as AWS CLI uses cryptographic signatures that include timestamps.

---

This setup allows you to securely manage AWS resources directly from your terminal using the AWS CLI.

### References

- https://accendnetworks.com/2024/11/10/how-to-configure-aws-cli-step-by-step-guide-for-beginners/

- https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-configure.html

- https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html

- https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html

- https://www.datacamp.com/tutorial/aws-cli-tutorial

- https://k21academy.com/amazon-web-services/aws-solutions-architect/aws-cli/

- https://www.microfocus.com/documentation/arcsight/arcsight-platform-22.1/arcsight-admin-guide-22.1/Content/deployment_cloud/AWS_CLI_configure.htm

- https://awscli.amazonaws.com/v2/documentation/api/latest/reference/configure/index.html

- https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-install.html

- https://www.youtube.com/watch?v=jCHOsMPbcV0

