# Installation

## 環境
* CentOS 7
* ansible 2.10

## ansible安裝步驟

### yum
```shell
sudo yum install epel-release
sudo yum install ansible
```

### pip
1. 安裝pip
```shell
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python get-pip.py
```

2. 安裝ansible
```shell
sudo python -m pip install ansible==2.10
```

3. 確認版本
```shell
ansible --version
```

## 參考資料
* [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-in-a-virtual-environment-with-pip)
