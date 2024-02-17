## Steps for How to Create AWS VPC

1. On AWS Console go to VPC
2. Click on Create VPC
   1. Select VPC Only
   2. Give Name
   3. Select IPV4 Manualinput and givw IPV4 CIDR - 10.0.0.0/16
   4. Tenancy - Default
   5. Create VPC
      
**We will be creating 2 subnet one in as public and other as private**

3. Create Public Subnet
   1. Go to Subnet section
   2. Create Subnet 
   3. VPC ID - Select our vpc
   4. Give public subnet name
   5. Availibility Zone preference (any)
   6. IPV4 Subnet CIDR block - 10.0.0.0/24

5. Create Private Subnet
   1. Go to Subnet section
   2. Create Subnet 
   3. VPC ID - Select our vpc
   4. Give public subnet name
   5. Availibility Zone preference (any) - ( **NOTE Select a different zone from public subnet** )
   6. IPV4 Subnet CIDR block - 10.0.1.0/24

  
6. Create Internet Gateway (IGW) -( **Required to connect subnet with outside world** )
   1. Go to Internet Gateways section
   2. Click on Create Internet gateway
   3. Give IGW name
   4. Create

7. Attach IGW to  VPC 
   1. Click on Action
   2. Select Attach to VPC
   3. Select our VPC
   4. Save

8. Create Route Tables for public subnet
   1. Go to Route Tables
   2. Click on Create route table
   3. Give public Route table name
   4. Select VPC
   5. Create route table

9. Create Route Tables for Private subnet
   1. Go to Route Tables
   2. Click on Create route table
   3. Give private Route table name
   4. Select VPC
   5. Create route table

10. Add Routing rules for Public Route table
    1.  Select Public Routetable
    2.  Click on  Routes tab shown below
    3.  Click on Edit Routes
    4.  Add Routes
    5.  Give 0.0.0.0/0
    6.  Target IGW
    7.  Save

**NOW our routing table for public is created but still we have to tell AWS where to route i.e. which subnet**              

10. Attach Public Subnet to Public Route table
    1. Click on Subnet Association
    2. Edit Subnet association
    3. Select public subnet
    4. Save associations
       
**Now our one part i.e. public part is completed**

12. Create NACL - to manage incoming and outgoung traffic (automatically create)
    
13. Create NAT gateway in public subnet
    1, Go to NAT gateway section
    1. Click on Create NAT gateway
    2. Associate Elastic IP (It will work as a public IP for NAT gateway. Unlike regular EC2 public IP this is a static IPv4 address provided by AWS which wont change unless you choose to release it)
    3. Repeat Step 9. Give private route table name,and Make sure to **Target NAT Gateway**
    4. Repeat Step 10. to Attach Private subnet with Private Route table
   
## NOW Create Ec2 Instance
### Take to EC2 Instance one i.e Jumpserver in our public subnet  and other in Private subnet###                               

### To do so when you create your EC2 instance for public i.e. Jumpserver###
1. in EC2 instance creation under Network setting
2. Click on Edit
3. Select our VPC.
4. Select subnet as public subnet
5. **Auto-assign public IP - Enable**

### For Private EC2 instance
1. In EC2 instance creation under Network setting
2. Click on Edit
3. Select our VPC.
4. Select subnet as private subnet
5. **Auto-assign public IP - DISABLE**

### Try to connect to both your instance and try to do 

```
sudo apt update
```

## _Congrats you have create your own Virtual Private Cloud_


  


      
