# Allow Snaplet to connect to an AWS RDS PostgreSQL Database

This document provides step-by-step instructions on how to grant and manage access to an AWS RDS PostgreSQL database. By following these instructions, you will be able to configure the necessary settings to establish a connection to your PostgreSQL database hosted on AWS RDS.

## Step 1: Configure Security Group

To allow access to your AWS RDS PostgreSQL database, you need to configure the associated security group to allow inbound connections to Snaplet's static IP addresses.

    1. Sign in to the AWS Management Console.
    2. Navigate to the AWS RDS service.
    3. Select "Databases" from the left-hand menu.
    4. Choose your PostgreSQL database instance from the list.
    5. In the "Connectivity & security" tab, locate the "Security" section.
    6. Click on the security group listed under "Security groups."
    7. You will be redirected to the Amazon VPC console.
    8. In the security group's "Inbound rules" tab, click "Edit inbound rules."
    10. Add a new rule for PostgreSQL by clicking "Add rule."
    Specify the following details:

    Type: PostgreSQL
    Port Range: 5432 (default PostgreSQL port)
    Source: Snaplet uses `3.67.57.100`, `3.68.126.236` and `35.158.181.77` to connect to your database. You will have to add each IP address as a seperate rule.

    Click "Save rules."

## Step 2: Add a read-only role

Add a read-only role by following our [PostgreSQL guide here.](/guides/postgresql#create-a-read-only-role)


## Conclusion

That's it! Snaplet is now able to capture snapshots.
