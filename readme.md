## virtualenv and django configuration
1. install virtualenv：
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py --force-reinstall
pip3 install virtualenv
pip3 install virtualenvwrapper
```
2. start virtualenv:
```
source virtualenvwrapper.sh
mkvirtualenv rango
workon rango
```
3. install django:`pip install -U django==1.9.10` 
## nginx and uwsgi configuration
1. install nginx: `sudo apt-get install nginx`
2. install uwsgi: `pip3 install uwsgi`
3. change the setting.py in django project:
  ```
  Debug = False
  Allow_host = ['your id', 'localhost',]
  STATIC_ROOT = os.path.join(BASE_DIR, 'collectedstatic')
  MEDIA_DIR = os.path.join(BASE_DIR, 'media')
  MEDIA_ROOT = MEDIA_DIR
  ```
4. Static file migration: `python manage.py collectstatic`
5. uwsgi configuration in ini way: build a mysite.ini under the same filedirection as the manage.py
6. nginx condiguartion: change the server{} in `/etc/nginx/nginx.conf ` `/etc/nginx/sites-enabled/default `
## run the whole project using uwsgi and nginx
1. start virtualenv:
```
source virtualenvwrapper.sh
workon rango
```
2. make sure every port is free to be used: `sudo fuser -k 8000/tcp`
3. start nginx & after changing the nginx.conf make sure you restart nginx: `sudo /etc/init.d/nginx restart`
4. start uwsgi:`uwsgi --ini mysite.ini`
5. run: `tail -f uwsgi.log`
