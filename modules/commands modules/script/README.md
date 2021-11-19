# script

- 用途：將本地script傳送到遠端主機之後執行

## 選項

| 參數      | 必要 | 預設值 | 選項   | 說明                                                                   |
| --------- | ---- | ------ | ------ | ---------------------------------------------------------------------- |
| chdir     | no   |        |        | 運行command命令前先cd到這個目錄                                        |
| creates   | no   |        |        | 如果這個參數對應的文件存在，就不運行command                            |
| decrypt   | no   | yes    | yes/no | 此選項控制使用vaule的source文件的自動解密                              |
| free_form | yes  |        |        | 需要執行腳本的本地文件路徑(沒有真正的參數叫free_form)                  |
| removes   | no   |        |        | 如果這個參數對應的文件不存在，就不運行command，與creates參數的作用相反 |

## 範例操作
1. cli格式
```shell
ansible host_name -m script -a "test.sh chdir=/tmp"
```

2. playbook格式
```yaml
# Example from Ansible Playbooks
- script: /some/local/script.sh --some-arguments 1234

# Run a script that creates a file, but only if the file is not yet created
- script: /some/local/create_file.sh --some-arguments 1234
  args:
    creates: /the/created/file.txt

# Run a script that removes a file, but only if the file is not yet removed
- script: /some/local/remove_file.sh --some-arguments 1234
  args:
    removes: /the/removed/file.txt
```

## 參考資料
* [script - Runs a local script on a remote node after transferring it — Ansible Documentation](https://docs.ansible.com/ansible/2.4/script_module.html#id1)
* [【Ansible学习】- 命令相关模块之expect, script, telnet模块 | hoxis' blog](https://hoxis.github.io/ansible-commands-modules-others.html)
## 相關module
* command
* shell
