# Image_recog_project_geni
## Install instructions
1.Clone the project from Github.

2.Use the rspec file "Image_recog_rspec.xml" to reserve the resource on GENI.

3.Once the slice is ready, find the routable ip by clicking node-1 and node-2, in my case 192.171.20.106 for node-1 and 192.171.20.107 for node-2.

4.Open /DLService/app.py and modify line 53 with your public ip of node-1, in my case:

    app.run(host="192.171.20.106")
    
5.Open /FrontEnd/webpage.html and modify line 19 with your public ip of node-1, in my case:

    url:"http://192.171.20.106:5000/predict"
    
6.Use scp to upload the /DLService folder to node-1 by following steps:

    1.Download winscp from https://winscp.net/eng/index.php and open winscp.
    
    2.Choose SCP under File protocol.
    
    3.Find your login information in GENI, for example：songxu@pcvm3-14.geni.case.edu.
    
    4.Enter host name, for example: pcvm3-14.geni.case.edu.
    
    5.Enter User name, for example：songxu.
    
    6.Default port number is 22.
    
    7.Go to Advanced -> SSH -> Authentication -> Private key file.
    
    8.Choose your putty key file(ppk format) and click open -> ok.
    
    9.Upload the /DLService folder to node-1.
    
7.SSH to node-1 (service node) and run the following commands(might take a few minutes):
```
    sudo apt update
    sudo apt-get install -y python3 python3-pip
    sudo apt install libjpeg-dev
    python3 -m pip install Pillow
    python3 -m pip install --no-cache-dir torch==1.7.0 torchvision==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
    python3 -m pip install flask
    python3 -m pip install -U flask-cors
    python3 app.py
 ```
8.Use scp to upload the /FrontEnd folder to node-2 as the steps shown above.

9.SSH to node-2 (front-end node) and configure static webpage by following steps:

    1.Enter the following commands:
``` 
        sudo apt update 
        sudo apt install nginx        
        sudo nano /etc/nginx/nginx.conf
```
    2.Under http part, find the line "default_type application/octet-stream;" and add the following code snippets below the previous line.
```
        server{
            listen 80;
            server_name <public ip of node-2>;
            root /users/<username>/FrontEnd;
            index webpage.html;
        }
```  
    3.Press Ctrl+O and Press enter.
    
    4.Run the following commands:
    
        sudo nginx -t
        
        sudo systemctl restart nginx
        
10.Open http://(public ip of node-2) in your browser, in my case http://192.171.20.107
