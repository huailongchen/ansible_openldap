# ansible_openldap
ansible deploy openldap

部署过程请参照下面方法：
下面过程都是在ansible-server端去操作
1、克隆代码
cd /etc/ansible/roles/
git clone https://github.com/huailongchen/ansible_openldap.git
mv ansible_openldap openldap
2、修改inventory.yml里面的ip地址为client端的ip
3、在ansible-server端创建SSH免交互登陆
ssh -keygen 命令输入完成之后一直回车，ls /root/.ssh/，会看到生成秘钥对，传输server端的公钥到client端上
如果一台服务器：
ssh-copy-id -i ansible-client服务器的ip
如果多台服务器：
vi ip.list，把ip写入到文件里
for a in `cat ip.list`;do ssh-copy-id -i $a;done
测试：
ansible ldap -i inventory.yml -m ping 看下节点通信是否正常
4、client端安装pexpect，因为在playbook会用到expect模块
①、安装epel源
yum -y install epel-release
②、安装pip
yum install -y python-pip
③、安装pexpect
pip install pexpect
5、执行playbook
ansible-playbook -i inventory.yml playbook.yml
6、访问phpldapadmin
http://IP/phpldapadmin
账号：cn=xxx,dc=xxx,dc=xxx
密码：xxxxxx

