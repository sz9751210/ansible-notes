# timezone

- 用途：設定系統時區

## 選項

| 參數    | 必要 | 預設值 | 選項 | 說明                                       |
| ------- | ---- | ------ | ---- | ------------------------------------------ |
| hwclock | no   |        |      | 系統硬體時鐘，可選本地或是UTC，可用別名RTC |
| name    | no   |        |      | 系統時區名稱                               |

## 範例操作
```yaml
- name: set timezone to Asia/Tokyo
  timezone:
    name: Asia/Taipei
```
## 參考資料
* [timezone - Configure timezone setting — Ansible Documentation](https://docs.ansible.com/ansible/2.4/timezone_module.html)

