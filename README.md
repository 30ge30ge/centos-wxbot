# centos-wxbot
1.先装依赖，查看openssl版本，小于3直接删掉 sudo yum remove openssl

2.官网下载openssL  https://www.openssl.org/source/index.html
下载好后，拖到/opt/文件夹里

3.安装依赖：
sudo yum -y install gcc perl-IPC-Cmd

yum install zlib* -y

yum install libffi-devel -y

4.cd 到openssl 文件夹
cd /opt/
解压
tar -zxvf openssl-3.2.1.tar.gz -C/opt

5.再cd 进   cd /opt/openssl-3.2.1/文件夹里
cd /opt/openssl-3.2.1/

./config


make


make install

6.共享
echo "/usr/local/lib64" >/etc/ld.so.conf.d/openssl.conf

ldconfig

openssl version

7.下载python
wget https://www.python.org/ftp/python/3.10.2/Python-3.10.2.tgz

8.移动路径
mv Python-3.10.2 /usr/local/
解压
tar -zxvf Python-3.10.2.tgz

9.cd 到解压文件夹
cd /usr/local/Python-3.10.2
配置编译
./configure --prefix=/usr/local/python310


make


make install

10.准备环境变量软链接
export PYTHON_HOME=/usr/local/python310

export PATH=$PATH:$PYTHON_HOME/bin

source /etc/profile

cd /usr/local/python310/bin
./pip3 -V

软链接
ln -s /usr/local/python310/bin/python3.10  /usr/bin/python3

ln -s /usr/local/python310/bin/pip3.10  /usr/bin/pip3

cd ~

python3

完成python3编译

#部署机器人

11.先安装git

sudo yum install git

12.clone
git clone https://github.com/zhayujie/chatgpt-on-wechat

13.cd到文件夹里
cd chatgpt-on-wechat/

14.安装依赖
pip3 install -r requirements.txt
pip3 install -r requirements-optional.txt

15.更改json文件
cp config-template.json config.json

16.运行
touch nohup.out
nohup python3 app.py & tail -f nohup.out
