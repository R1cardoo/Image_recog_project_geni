apt-get install -y python3 python3-pip
python3 -m pip install torch==1.7.0 torchvision==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
python3 -m pip install flask

python3 app.py
