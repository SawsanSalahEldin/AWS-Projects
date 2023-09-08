A basic CRUD app that serves as an Employee Directory, allowing users to create, read, update, and delete employee records within a company.

## Functionality

- **Create**: Users can create new employee records by providing relevant information such as name, position, and contact details.

- **Read**: Users can view the list of existing employees and access individual employee profiles for detailed information.

- **Update**: Users can modify employee records, updating details such as position, contact information, or other relevant fields.

- **Delete**: Users can remove employee records from the directory, permanently deleting their information.


![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/4a64659b-ec8f-420d-b453-a11ba5b79af9)


Login to an AWS account using a user with admin privileges and ensure your region is set to us-east-1 N. Virginia

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
          

