# face-attendance-web-app-react-python
## Back-end setup
In Amazon EC2, launching a instance. Naming it to face-attendance-web-app-backend, using Ubuntu server 22.04 LTS(HVM) version, using t3.2xlarge instance type and creating key pair.

In the terminal, type this code

    ssh -i ~/ <PATH_TO_KEY_PAIR> ubuntu <PUBLIC_IPv4_DNS>

SSH into the instance and run these commands to update the software repository and install the dependencies.

    sudo apt-get update
    sudo apt install -y python3-pip nginx

Open and update faspi_nginx file then save the file

    sudo nano /etc/nginx/sites-enabled/fastapi_nginx

Put this configuration into that file to replace the IP address with EC2 instance's public IP

    server {
        listen 80;   
        server_name <PUBLIC_IP>;    
        location / {        
            proxy_pass http://127.0.0.1:8000;    
        }
    }

restart service nginx file to get updated file 

    sudo service nginx restart

Update EC2 security-group settings by cilck on the securiry button then add inbound rule to your instance to allow HTTP traffic to port 80.

## Launch API endpoints of backend

Cloning the GitHub repository
 
    git clone https://github.com/P2687532/face-attendance-web-app-react-python.git
   
    cd face-attendance-web-app-react-python

Install Python 3.8, create a virtual environment and install requirements.

    sudo apt update

    sudo apt install software-properties-common

    sudo add-apt-repository ppa:deadsnakes/ppa

    sudo apt install python3.8

    sudo apt install python3.8-dev

    sudo apt install python3.8-distutils

    sudo apt install python3-virtualenv
    
    cd backend

    virtualenv venv --python=python3.8

    source venv/bin/activate
    
    pip install cmake==3.25.0

    pip install dlib==19.18.0

    pip install -r requirements.txt

Launch the backend web app

    python3 -m uvicorn main:app

## Front-end setup
In Amazon EC2, launching a new instance. Naming it to face-attendance-web-app-frontend, using Ubuntu server 22.04 LTS(HVM)version, using t3xlarge instance type and creating key pair.
In the terminal, type this code

    ssh -i ~/ <PATH_TO_KEY_PAIR> ubuntu <PUBLIC_IPv4_DNS>

SSH into the instance and run these commands to update the software repository and install the dependencies.

    sudo apt-get update
    sudo apt install -y python3-pip nginx

Open and update faspi_nginx file then save the file

    sudo nano /etc/nginx/sites-enabled/fastapi_nginx

Put this configuration into that file to replace the IP address with EC2 instance's public IP

    server {
        listen 80;   
        server_name <PUBLIC_IP>;    
        location / {        
            proxy_pass http://127.0.0.1:3000;    
        }
    }

restart service nginx file to get updated file

    sudo service nginx restart

Update EC2 security-group settings by cilck on the securiry button then add inbound rule to your instance to allow HTTP traffic to port 80.

## Launch API endpoints of front-end
Cloning the GitHub repository
 
    git clone https://github.com/P2687532/face-attendance-web-app-react-python.git
   
    cd face-attendance-web-app-react-python
    
    cd frontend/face-attendance-web-app-front/
    
    sudo apt-get install npm
    
    npm install

Edit the value of __API_BASE_URL__ in src/API.js with the ip of the backend server.
    
    nano src/API.js

start
    
    npm start

ou may need to adjust your browser to allow access to your webcam through an unsecure conection from the EC2 ip address. In chrome this setting is adjusted here __chrome://flags/#unsafely-treat-insecure-origin-as-secure__