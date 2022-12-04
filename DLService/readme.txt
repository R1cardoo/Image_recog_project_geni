sudo apt-get install -y python3 python3-pip
sudo apt install libjpeg-dev
python3 -m pip install Pillow
python3 -m pip install --no-cache-dir torch==1.7.0 torchvision==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
python3 -m pip install flask
python3 -m pip install -U flask-cors
python3 app.py
