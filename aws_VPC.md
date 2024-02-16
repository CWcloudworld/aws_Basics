## Steps for How to Create AWS VPC

1. On AWS Console go to VPC
2. Click on Create VPC
   1. Give  Manual CIDR block - 10.0.0.0/16
   2. Create
      
**We will be creating 2 subnet one in as public and other as private**

3. Create Public Subnet 
   1. Select our vpc
   2. Click on on Create Subnet and give public subnet name
   3. Availibility Zone preference.
   4. Select CIDR block 10.0.0.0/24

4. Create Private Subnet
   1. Select our vpc
   2. Click on on Create Subnet and give private subnet name
   3. Availibility Zone preference ( **NOTE Select a different zone from public subnet** ).
   4. Select CIDR block 10.0.1.0/24
  
5. Create Internet Gateway (IGW)
   1. Go to IGW
   2. Give IGW name
   3. Create

6. Attach IGW to  VPC ( **Required to connect subnet with outside world** )
   1. Click on Action
   2. Select VPC
   3. Save

7. Create Route Tables for public subnet
   1. Go to Route Tables
   2. Give Route table name
   3. Select VPC
   4. Create

8. Create Route Tables for Private subnet
   1. Go to Route Tables
   2. Give Route table name
   3. Select VPC
   4. Create

9. Add Routing rules
    1.  Select Public Routetable
    2.  Click on Edit
    3.  Add Routes
    4.  Give 0.0.0.0/0
    5.  Target IGW
    6.  Save

**NOW our routing table for public is created but still be have to AWS him where to route i.e. which subnet**              

10. Attach Public Subnet to Public Route table
    1. Click on Subnet Association
    2. Edit Subnet association
    3. Select public subnet
    4. Save
       
**Now our one part i.e. public part is completed**

12. Create NACL - to manage incoming and outgoung traffic (automatically create)
    
13. Create NAT gateway in public subnet 
    1. Click on Create NAT
    2. Associate Elastic IP (It will work as a public IP for NAT gateway. Unlike regular EC2 public IP this is a static IPv4 address provided by AWS which wont change unless you choose to release it)
    3. Repeat Step 9. Give private route table name,and Make sure to **Target NAT Gateway**
    4. Repeat Step 10. to Attach Private subnet with Private Route table
   
## NOW Create Ec2 Instance
### Take to EC2 Instance one i.e Jumpserver in our public subnet  and other in Private subnet###                               

### To do so when you create your EC2 instance for public i.e. Jumpserver###
1. in EC2 instance creation under Network setting in VPC, select our VPC
2. Then select subnet our public subnet

### For Private EC2 instance
1. Select our VPC and then  select our Private subnet
  


      
