# command

- 用途：在遠端主機上執行指令

## 選項

| 參數      | 必要    | 預設值 | 選項   | 說明                                                                                            |
| --------- | ------- | ------ | ------ | ----------------------------------------------------------------------------------------------- |
| chdir     | no      |        |        | 在執行指令之前先切換到指定路徑                                                                  |
| creates   | np      |        |        | 如果這個參數對應的文件存在，就不運行command                                                     |
| free_form | yes     |        |        | 需要執行的腳本，也就是命令                                                                      |
| removes   | removes |        |        | 如果這個參數對應的文件不存在，就不運行command，與creates參數的作用相反                          |
| stdin     | no      |        |        | 將命令的stdin設置為指定的值                                                                     |
| warn      | no      | yes    | yes/no | If command_warnings are on in ansible.cfg, do not warn about this particular line if set to no. |

## 範例操作
1. cli格式
```shell
ansible host_name -m command -a "ls" --ask-pass --ask-become-pass -vvv
```

2. playbook格式
```yaml
- name: 將cat出來的結果註冊為mymotd變數的內容
  command: cat /etc/motd
  register: mymotd

- name: 當/path/to/database不存在才會執行
  command: /usr/bin/make_database.sh arg1 arg2 creates=/path/to/database

# You can also use the 'args' form to provide the options.
- name: 此指令會先進入somedir/接著確認/path/to/database是否存在，不存在才會執行指令
  command: /usr/bin/make_database.sh arg1 arg2
  args:
    chdir: somedir/
    creates: /path/to/database

- name: safely use templated variable to run command. Always use the quote filter to avoid injection issues.
  command: cat {{ myfile|quote }}
  register: myoutput
```
## 參考資料
* [command - Executes a command on a remote node](https://docs.ansible.com/ansible/2.4/command_module.html)
* [【Ansible学习】- 命令相关模块之command, shell, raw模块](https://hoxis.github.io/ansible-commands-modules-command-shell-raw.html)
## 相關module
* shell
