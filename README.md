## How to deploy a new react app using nginx

`=============================================================================================`

## Uploading the react app to the server

`=============================================================================================`

### Step 1

SSH into the server

`ssh root@ipaddress`

### Step 2

Create project directory

`cd /home/`
`mkdir projectName`
`cd projectName`

### Step 3

Clone the repository from github

`git clone linkToTheRepo`

### Step 4

Test if the node version on the server is compatible with the version being used by your code
`npm install`
`npm start `

### Step 5

Build the react app files

`npm run build`

### Step 6

Create a folder to store the static files

`mkdir /var/www/myProject`

Copy the build file to a

`sudo cp -R build/ /var/www/myProject/`


`=============================================================================================`

## Setting up NGINX

`=============================================================================================`

### Step 1

Navigate to the sites-enabled folder

`cd /etc/nginx/sites-enabled`

### Step 2

Create a file where you will store your apps configs

`sudo touch myAppName`

### Step 3

Open the file

`sudo nano myAppName`

### Step 4

Copy these configs

```
server {
        listen  80;
        server_name MY_IP_ADDRESS;
        location / {
                root /var/www/myProject/build;
                index index.html;
                try_files $uri $uri/ /index.html?$args;
        }
}

```

ctrl x and save the file

### Step 5

Sync the build file with the static files in /var/www/

` sudo rsync -a build/ /var/www/myProject/build/`

### Step 6

Restart nginx

`sudo service nginx restart`
