配置新网站
=========================

## 需要的包

* nginx
* Python 3.6
* virtualenv + pip
* Git

以Ubuntu为例
    
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt-get update
    sudo apt-get install nginx git python3.6 python3.6-venv

## Nginx虚拟主机

* 参考nginx.template.conf
$ sed "s/SITENAME/tyrone-zhao.club/g" source/deploy_tools/nginx.template.conf | sudo tee /etc/nginx/sites-available/tyrone-zhao.club
$ sudo ln -s /etc/nginx/sites-available/tyrone-zhao.club /etc/nginx/sites-enabled/tyrone-zhao.club

$ sed "s/SITENAME/116.85.48.20/g" source/deploy_tools/nginx.template.conf | sudo tee /etc/nginx/sites-available/tyrone-zhao.club
$ sudo ln -s /etc/nginx/sites-available/tyrone-zhao.club /etc/nginx/sites-enabled/tyrone-zhao.club

* 把SITENAME替换成所需的域名，例如staging.my-domain.com

## Systemd服务

* 参考gunicorn-systemd.template.service
$ sed "s/SITENAME/tyrone-zhao.club/g" source/deploy_tools/gunicorn-systemd.template.service | sudo tee /etc/systemd/system/gunicorn-tyrone-zhao.club.service
$ sudo systemctl daemon-reload
$ sudo systemctl reload nginx
$ sudo systemctl enable gunicorn-tyrone-zhao.club.service 
$ sudo systemctl start gunicorn-tyrone-zhao.club.service 

$ sed "s/SITENAME/116.85.48.20/g" source/deploy_tools/gunicorn-systemd.template.service | sudo tee /etc/systemd/system/gunicorn-tyrone-zhao.club.service
$ sudo systemctl daemon-reload
$ sudo systemctl reload nginx
$ sudo systemctl enable gunicorn-tyrone-zhao.club.service 
$ sudo systemctl start gunicorn-tyrone-zhao.club.service 

* 把SITENAME替换成所需的域名，例如staging.my-domain.com

## 文件夹结构：
假设有用户账户，家目录为/home/username

/home/username
`-- sites
    `-- SITENAME
        |-- database
        |-- source
        |-- static
        `-- virtualenv