psql --host auth-api.cd8ggqv3baa9.us-east-2.rds.amazonaws.com --username kana --dbname postgres

create database authapi; create database authapi_test;


--- if ssh key too open

$path = ".\auth-api-app-server.pem"
# Reset to remove explicit permissions
icacls.exe $path /reset
# Give current user explicit read-permission
icacls.exe $path /GRANT:R "$($env:USERNAME):(R)"
# Disable inheritance and remove inherited permissions
icacls.exe $path /inheritance:r

ssh -i "auth-api-app-server.pem" ubuntu@ec2-3-135-191-239.us-east-2.compute.amazonaws.com

--- inside ec2
curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

node -v

sudo npm install pm2 -g

pm2 start npm --name "auth-api" -- run "start"