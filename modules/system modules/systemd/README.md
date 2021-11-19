# systemd

- 用途：管理service

## 選項

| 參數          | 必要 | 預設值 | 選項                               | 說明                                                                      |
| ------------- | ---- | ------ | ---------------------------------- | ------------------------------------------------------------------------- |
| daemon_reload | no   |        | yes/no                             | 在執行任何其他操作之前運行守護進程重新加載，以確保systemd已經讀取其他更改 |
| enabled       | no   |        | yes/no                             | 服務是否開機自動啟動。 enabled和state至少要有一個被定義                   |
| masked        | no   |        | yes/no                             | 是否將服務設置為masked狀態，被mask的服務是無法啟動的                      |
| name          | no   |        |                                    | 服務名稱                                                                  |
| no_block      | no   |        | yes/no                             | 不要同步等待操作請求完成                                                  |
| state         | no   |        | started/stopped/restarted/reloaded | service最終操作後的狀態                                                   |
| user          | no   |        | yes/no                             | 使用服務的調用者運行systemctl，而不是系統的服務管理者                     |


## 範例操作
1. cli格式
```shell
ansible host_name -m systemd -a "name=httpd state=started"
```

2. playbook格式
```shell
- name: 啟動httpd服務
  systemd: state=started name=httpd

- name: 停止cron服務
  systemd: name=cron state=stopped

- name: restart service cron on centos, in all cases, also issue daemon-reload to pick up config changes
  systemd:
    state: restarted
    daemon_reload: yes
    name: crond

- name: reload httpd服務
  systemd:
    name: httpd
    state: reloaded

- name: enable service httpd and ensure it is not masked
  systemd:
    name: httpd
    enabled: yes
    masked: no

- name: enable a timer for dnf-automatic
  systemd:
    name: dnf-automatic.timer
    state: started
    enabled: True

- name: just force systemd to reread configs (2.4 and above)
  systemd: daemon_reload=yes
```

## 參考資料
* [systemd - Manage services.](https://docs.ansible.com/ansible/2.4/systemd_module.html)
* [【Ansible学习】- 常用系统模块之service/systemd/ping模块](https://hoxis.github.io/ansible-system-modules.html)
## 相關module
* service
