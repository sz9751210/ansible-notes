# service

- 用途：管理service

## 選項

| 參數      | 必要 | 預設值  | 選項                               | 說明                                                                                                                                                                                                                                                                      |
| --------- | ---- | ------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| arguments | no   |         |                                    | 如果打開這個標記，backrefs會改變模塊的一些操作：insertbefore和insertafter參數會被忽略。當regexp不匹配文件中的任何行時，文件不會做任何修改，否則 使用擴展的line參數 替換 最後一個匹配正則表達式的行                                                                        |
| enabled   | no   |         | yes/no                             | 服務是否開機自動啟動。 enabled和state至少要有一個被定義                                                                                                                                                                                                                   |
| name      | yes  |         |                                    | 服務名稱                                                                                                                                                                                                                                                                  |
| pattern   | no   |         |                                    | 如果服務沒有響應，則ps查看是否具有指定參數的進程，有則認為服務已經啟動                                                                                                                                                                                                    |
| runlevel  | no   | default |                                    | For OpenRC init scripts (ex: Gentoo) only. The runlevel that this service belongs to.                                                                                                                                                                                     |
| sleep     | no   |         |                                    | 如果服務正在重新啟動，則在停止和啟動命令之間定義休眠幾秒                                                                                                                                                                                                                  |
| state     | no   |         | started/stopped/restarted/reloaded | service最終操作後的狀態                                                                                                                                                                                                                                                   |
| use       | no   | auto    |                                    | The service module actually uses system specific modules, normally through auto detection, this setting can force a specific module. Normally it uses the value of the 'ansible_service_mgr' fact and falls back to the old 'service' module when none matching is found. |

## 範例操作
```yaml
# 如果沒啟動httpd服務的話則啟動它
- service:
    name: httpd
    state: started

# 如果啟動httpd服務的話則停止它
- service:
    name: httpd
    state: stopped

# 重啟httpd服務
- service:
    name: httpd
    state: restarted

# reload httpd服務
- service:
    name: httpd
    state: reloaded

# 設定httpd開機自啟動
- service:
    name: httpd
    enabled: yes

# 根據pattern啟動foo進程
- service:
    name: foo
    pattern: /usr/bin/foo
    state: started

# 重啟network的eth0網卡
- service:
    name: network
    state: restarted
    args: eth0
```
## 參考資料
* [service - Manage services.](https://docs.ansible.com/ansible/2.4/service_module.html)
* [【Ansible学习】- 常用系统模块之service/systemd/ping模块](https://hoxis.github.io/ansible-system-modules.html)
## 相關module(可選)
* systemd
