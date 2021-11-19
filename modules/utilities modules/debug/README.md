# debug

- 用途：在調試中輸出訊息，方便debug

## 選項

| 參數      | 必要 | 預設值       | 選項 | 說明                                                                                |
| --------- | ---- | ------------ | ---- | ----------------------------------------------------------------------------------- |
| msg       | no   | Hello world! |      | 要顯示的訊息                                                                        |
| var       | no   |              |      | 將某個任務執行的輸出作為變量傳遞給debug模塊，debug會直接將其打印輸出，與msg選項互斥 |
| verbosity | no   |              |      | debug的等級，0為輸出全部                                                            |



## 範例操作
1. cli格式
```shell
ansible host_name -m debug

ansible host_name -m debug -a "msg=test"
```

2. playbook格式
```yaml
# Example that prints the loopback address and gateway for each host
- debug:
    msg: "System {{ inventory_hostname }} has uuid {{ ansible_product_uuid }}"

- debug:
    msg: "System {{ inventory_hostname }} has gateway {{ ansible_default_ipv4.gateway }}"
  when: ansible_default_ipv4.gateway is defined

- shell: /usr/bin/uptime
  register: result

- debug:
    var: result
    verbosity: 2

- name: Display all variables/facts known for a host
  debug:
    var: hostvars[inventory_hostname]
    verbosity: 4
```
## 參考資料
* [debug - Print statements during execution — Ansible Documentation](https://docs.ansible.com/ansible/2.4/debug_module.html)
* [debug模块 · ansible · 看云 (kancloud.cn)](https://www.kancloud.cn/willseecloud/ansible/1472264)
* [ansible小结（十 三）playbook中使用debug模块 – 运维之路 (361way.com)](https://www.361way.com/ansible-playbook-debug/5481.html)

