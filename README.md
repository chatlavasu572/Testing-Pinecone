# Testing-Pinecone in Service Catalog 
## Firstly Creating a DUMMY-INSTANCE named DUMMMY_PINECONE in the AWS_CONSOLE.

![Screenshot from 2025-06-22 10-47-13](https://github.com/user-attachments/assets/3abfbc08-da04-4f28-9420-3e9f6465c01e)

## Next iam taking Ubutu OS AMI for launching an instance 

![Screenshot from 2025-06-22 10-47-13](https://github.com/user-attachments/assets/1c82914e-87c0-4425-987d-0976c4732f3b)

## Instance Type :t2.micro


![Screenshot from 2025-06-22 10-47-13](https://github.com/user-attachments/assets/25b75a29-a6fb-41f0-987a-f80793fed556)

## KeyPair Login 
create a key pair for connecting ssh-clinet to the local terminal 
![Screenshot from 2025-06-22 10-49-29](https://github.com/user-attachments/assets/e1faadd2-0fdf-4e35-a936-36dbade6c3dd)


## Network Settings 
allowing all HTTP,HTTPs,SSH traffic

![Screenshot from 2025-06-22 10-50-19](https://github.com/user-attachments/assets/9b3c46b8-807f-4709-88c0-38371c2cef87)

## now launch an instance click on connect for conecting to the terminal in your local-machine with he help of ssh-clinet.


![Screenshot from 2025-06-22 11-02-18](https://github.com/user-attachments/assets/17312c8d-7f64-4777-8028-eca192708d5d)

##  now connect to the instance using browser based client

![Screenshot from 2025-06-22 11-02-31](https://github.com/user-attachments/assets/c06f1145-046a-45ab-b839-6c7cb136f917)

```
ssh -i "pineconekeypair.pem" ubuntu@ec2-13-233-98-208.ap-south-1.compute.amazonaws.com
```
![Screenshot from 2025-06-22 11-30-45](https://github.com/user-attachments/assets/f6adff91-29ee-49f3-8006-7b9de70a99fc)


## now open browser search for PINECONE web ui : https://app.pinecone.io/ 

## 🔐 Why Do You Need a Pinecone API Key?
### The Pinecone API key is required to:

- Authenticate your app or script

- Authorize access to your Pinecone account and indexes

- Track usage (read/write units) and billing

- Ensure security — so no one else can access your data without permission

![Screenshot from 2025-06-22 11-11-12](https://github.com/user-attachments/assets/3f4d8dab-d5c8-46de-8610-d06ced903c17)

now Iam Creating a pinecone API KEY :

![Screenshot from 2025-06-22 11-16-55](https://github.com/user-attachments/assets/628eb936-24a4-42b5-a6c9-18beefcf017e)

## ✅ Step-by-Step Guide to Install and Use Pinecone on Ubuntu

### 1. Install Python (if not installed)
```
sudo apt update
sudo apt install python3 python3-pip -y
```
### 2. Create and Activate a Virtual Environment
```
python3 -m venv pinecone-env
source pinecone-env/bin/activate
```
### 3. Install Pinecone Python Client
```
pip install pinecone-client
```







