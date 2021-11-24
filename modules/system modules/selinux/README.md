# selinux

- 用途：設定selinux模式和策略

## 選項

| 參數   | 必要 | 預設值              | 選項                          | 說明                                                                                            |
| ------ | ---- | ------------------- | ----------------------------- | ----------------------------------------------------------------------------------------------- |
| conf   | no   | /etc/selinux/config |                               | SElinux的設定檔路徑                                                                             |
| policy | no   |                     |                               | name of the SELinux policy to use (example: targeted) will be required if state is not disabled |
| state  | yes  |                     | enforcing/permissive/disabled | SElinux的模式                                                                                   |

## 範例操作
```yaml
# 開啟SELinux
- selinux:
    policy: targeted
    state: enforcing

# Put SELinux in permissive mode, logging actions that would be blocked.
- selinux:
    policy: targeted
    state: permissive

# 關閉SELinux
- selinux:
    state: disabled
```

> selinux模式介紹
> - enforcing：強制開啟selinux
> - permissive：selinux運行中，會有告警訊息，但實際不會限制
> - disabled：關閉，selinux没有運行
## 參考資料
* [selinux - Change policy and state of SELinux — Ansible Documentation](https://docs.ansible.com/ansible/2.4/selinux_module.html)
* [selinux模块 - ansible (gitbook.io)](https://pshizhsysu.gitbook.io/ansible/ansiblemo-kuai/selinuxmo-kuai)
