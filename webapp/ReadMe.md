A basic CRUD app that serves as an Employee Directory, allowing users to create, read, update, and delete employee records within a company.

## Functionality

- **Create**: Users can create new employee records by providing relevant information such as name, position, and contact details.

- **Read**: Users can view the list of existing employees and access individual employee profiles for detailed information.

- **Update**: Users can modify employee records, updating details such as position, contact information, or other relevant fields.

- **Delete**: Users can remove employee records from the directory, permanently deleting their information.


![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/4a64659b-ec8f-420d-b453-a11ba5b79af9)


Login to an AWS account using a user with admin privileges and ensure your region is set to us-east-1 N. Virginia

**Task1**

**Setting up an IAM role for an EC2 instance**

In this task, you will log in as the *Admin* user and create an IAM role. The role allows Amazon Elastic Compute Cloud (Amazon EC2) to access both Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB. You will later assign this role to an EC2 instance that hosts the employee directory application.

1. Now that you are logged in as the *Admin* user, use the **Services** search bar to search for **IAM** again, and open the service by choosing **IAM**.
2. In the navigation pane, choose **Roles**.
3. Choose **Create role**.
4. In the **Select trusted entity** page, configure the following settings.
    - **Trusted entity type**: *AWS service*
    - **Use case**: *EC2*
5. Choose **Next**.
6. In the permissions filter box, search for `amazons3full`, and select **AmazonS3FullAccess**.
7. In the filter box, search for `amazondynamodb`, and select **AmazonDynamoDBFullAccess**.
8. Choose **Next**.
9. For **Role name**, paste `S3DynamoDBFullAccessRole` and choose **Create role**.
   ![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/547d3c67-f3af-4c20-bdae-e0295e4816ef)

   ================================================================

 **Task2**
 
 **Setting up a VPC**
In this scenario, you create the underlying network infrastructure where the EC2 instance that hosts the employee directory will live.

 you set up a new virtual private cloud (VPC). This new VPC will have twosubnets (two public subnets  and two route tables ( public route table) 
In this task, you will create a new VPC.

1. If needed, log in to the AWS Management Console as your *Admin* user.
2. In the **Services** search box, enter `VPC` and open the VPC console by choosing **VPC** from the list.
3. In the navigation pane, under **Virtual private cloud**, choose **Your VPCs**.
4. Choose **Create VPC**.
5. Configure these settings:
    - **Name tag**: `app-vpc`
    - **IPv4 CIDR block**: `10.1.0.0/16`


 ![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/ce636e9a-61e4-496e-8468-11240eaf71e3)

 
  **Creating Internet gateways**

1. In the navigation pane, under **Virtual private cloud**, choose **Internet gateways**
2. Choose **Create internet gateway**.
3. For **Name tag**, paste `app-igw` and choose **Create internet gateway**.
4. In the details page for the internet gateway, choose **Actions** and then choose **Attach to VPC**.
5. For **Available VPCs**, choose `app-vpc` and then choose **Attach internet gateway**.

 **Creating subnets**

In this task, you will create the four subnets for your VPC. You will configure the two public subnets first, and then configure the two private subnets.

1. From the navigation pane, choose **Subnets**.
2. Choose **Create subnet**.
3. For the first public subnet, configure these settings:
    - **VPC ID**: *app-vpc*
    - **Subnet name**:`Public Subnet 1`
    - **Availability Zone**: Choose the first Availability Zone
        - Example: If you are in US West (Oregon), you would choose *us-west-2a*
    - **IPv4 CIDR block**: `10.1.1.0/24`
4. Choose **Add new subnet**.
5. For the second public subnet, configure these settings:
    - **Subnet name**: `Public Subnet 2`
    - **Availability Zone**: Choose the second Availability Zone
        - Example: If you are in US West (Oregon), you would choose *us-west-2b*
        - **IPv4 CIDR block**: 10.1.2.0/24
          
6. After the subnets are created, select the check box for **Public Subnet 1**.
7. Choose **Actions** and then choose **Edit subnet settings**.
8. For **Auto-assign IP settings**, select **Enable auto-assign public IPv4 address** and then choose **Save**.
9. Clear the check box for **Public Subnet 1** and select the check box for **Public Subnet 2**.
10. Again, choose **Actions** and then **Edit subnet settings**.11
11. . For **Auto-assign IP settings**, select **Enable auto-assign public IPv4 address** and save the settings.

**Creating route tables**

In this task, you will create the route tables for your VPC.

First, you will create the public route table.

1. In the navigation pane, choose **Route Tables**.
2. Choose **Create route table**.
3. For the route table, configure these settings:
    - **Name**: `app-routetable-public`
    - **VPC**: *app-vpc*
4. Choose **Create route table**.
5. If needed, open the route table details pane by choosing **app-routetable-public** from the list
6. 1. Choose the **Routes** tab and choose **Edit routes**.
7. Choose **Add route** and configure these settings:
    - **Destination**: `0.0.0.0/0`
    - **Target**: *Internet Gateway*, then choose *app-igw* (which you set up in the VPC task)
8. Choose **Save changes**.
9. Choose the **Subnet associations** tab.
10. Scroll to **Subnets without explicit associations** and choose **Edit subnet associations**.
11. Select the two public subnets that you created (**Public Subnet 1** and **Public Subnet 2**) and choose **Save associations**.
![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/af2148ff-e746-4696-a607-0f8ee33be646)

==============================================================

 **Task3**


**Creating an S3 Bucket and Modifying the EC2 Instance**

For this scenario, you create the S3 bucket where the employee photos will be stored.

In this exercise, you create the S3 bucket, upload an object to it, and modify the bucket policy. You also launch an EC2 instance with updated user data so that the application uses the S3 bucket. Finally, you stop the EC2 instance to prevent future costs.

 **Creating an S3 bucket**

In this task, you will create an S3 bucket.

1. If needed, log in to the AWS Management Console with your *Admin* user.
2. In the search box, enter `S3` and open the Amazon S3 console by choosing **S3**.
3. Choose **Create bucket**.
4. For **Bucket name**, enter `employee-photo-bucket-<your initials>-<unique number>`.    
5. Choose **Create bucket**.
**Uploading a photo**


In this task, you will upload an object (a photo) to the S3 bucket.

1. Open the details of your newly created bucket by choosing the bucket name.
2. Choose **Upload**.
3. Choose **Add files**.
4. Choose a photo of your choice from your computer and choose **Open**.
5. Choose **Upload.**
    
    At the top, you should see *Upload succeeded* in green.
    
6. Choose **Close**.

 **Modifying the S3 bucket policy**

In this task, you will update the bucket policy. The updated configuration allows the IAM role that you created previously to access the bucket.

1. Choose the **Permissions** tab.
2. Scroll down to **Bucket policy** and choose **Edit**.
3. In the box, paste the following policy:
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowS3ReadAccess",
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::<INSERT-ACCOUNT-NUMBER>:role/S3DynamoDBFullAccessRole"
                },
                "Action": "s3:*",
                "Resource": [
                    "arn:aws:s3:::<INSERT-BUCKET-NAME>",
                    "arn:aws:s3:::<INSERT-BUCKET-NAME>/*"
                ]
            }
        ]
    
    ```
    
4. Replace the `<INSERT-ACCOUNT-NUMBER>` placeholder with your account number.
5. Replace the `<INSERT-BUCKET-NAME>` placeholder with your bucket name.     
6. Choose **Save changes**.



==============================================================

 **Task4**

 
 
 **Creating the DynamoDB table**

To connect the application to a database, you first need to create one! In this task, you will create a database by using DynamoDB.

1. Return to the console, and search for and open **DynamoDB**.
2. In the navigation pane, choose **Tables**.
3. Choose **Create table** and configure the following settings.
    - **Table name**: `Employees`
    - **Partition key**: `id`
4. Choose **Create table**.

==============================================================

 **Task5**
 **Creating EC2**
 
## Launching an EC2 instance that uses a role

In this task, you will launch an EC2 instance that hosts the employee directory application.

1. If needed, log in to the AWS Management Console as your *Admin* user.
2. In the **Services** search bar, search for **EC2**, and open the service by choosing **EC2**.
3. In the navigation pane, under **Instances** choose **Instances**.
4. Choose **Launch instances**.
5. For **Name** use `employee-directory-app`.
6. Under **Application and OS Images (Amazon Machine Image)**, choose the default **Amazon Linux 2023**.
7. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/191ca721-e08f-4a65-b4c6-6a8fd47b8eb2/Untitled.png)

1. Under **Instance type**, select **t2.micro**.
2. Under **Key pair (login)**, choose **Create a new key pair**.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f9b0e3af-9f96-47f1-8721-f4c7bea1f6b3/Untitled.png)

1. For **Key pair name**, paste `app-key-pair`. Choose **Create key pair**. The required **.pem** file should automatically download for you.
2. Under **Network settings** and **Edit**: Keep the default VPC selection, which should have *(default)* after the network name
    - **Subnet**: Choose the first subnet in the dropdown list
    - **Auto-assign Public IP**: *Enable*
3. Under **Firewall (security groups)** choose **Create security group** use `app-sg` for the **Security group name** and **Description**.
4. Under **Inbound security groups rules** choose **Remove** above the **ssh** rule.
5. Choose **Add security group rule**. For **Type** choose **HTTP**. Under **Source type** choose **Anywhere**.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3797788c-b1f0-4a54-a228-64db081bf2ed/Untitled.png)

1. Expand **Advanced details** and under choose **S3DynamoDBFullAccessRole**.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bdf9fcb4-217d-4afc-b176-c03c94256f01/Untitled.png)

1. In the **User data** box, paste the following code:
    
    ```bash
    #!/bin/bash -ex
    wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip
    unzip FlaskApp.zip
    cd FlaskApp/
    yum -y install python3-pip
    pip install -r requirements.txt
    yum -y install stress
    export PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}
    export AWS_DEFAULT_REGION=<INSERT REGION HERE>
    export DYNAMO_MODE=on
    FLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80
    ```

    
![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/6498bfac-bdcf-4a63-9f5d-867faef04806)
![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/11799db5-9b41-4046-938f-8068290e8284)


    
    Example:
    
    The following example uses the US West (Oregon) Region, or *us-west-2*.
    
    ```bash
    export AWS_DEFAULT_REGION=us-west-2
In the user data code, replace the PHOTOS_BUCKET placeholder value with the name of your bucket.

Example:
```bash
export PHOTOS_BUCKET=
    
3. Choose **Launch instance**.
4. Choose **View all instances**.
    
    The instance should now be listed under **Instances**.
    
5. Wait for the **Instance state** to change to *Running* and the **Status check** to change to *2/2 checks passed*.
