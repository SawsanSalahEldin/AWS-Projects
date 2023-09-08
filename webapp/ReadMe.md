A basic CRUD app that serves as an Employee Directory, allowing users to create, read, update, and delete employee records within a company.

## Functionality

- **Create**: Users can create new employee records by providing relevant information such as name, position, and contact details.

- **Read**: Users can view the list of existing employees and access individual employee profiles for detailed information.

- **Update**: Users can modify employee records, updating details such as position, contact information, or other relevant fields.

- **Delete**: Users can remove employee records from the directory, permanently deleting their information.


![image](https://github.com/SawsanSalahEldin/AWS-Projects/assets/108637290/4a64659b-ec8f-420d-b453-a11ba5b79af9)


Login to an AWS account using a user with admin privileges and ensure your region is set to us-east-1 N. Virginia

1- **Setting up an IAM role for an EC2 instance**

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



