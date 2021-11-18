# copy

- 用途：複製本地目錄或是檔案到遠端

## 選項

| 參數           | 必要 | 預設值 | 選項   | 說明                                                                                                                                                                                                                   |
| -------------- | ---- | ------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| attributes     | no   | none   |        | Attributes the file or directory should have. To get supported flags look at the man page for chattr on the target system. This string should contain the attributes in the same order as the one displayed by lsattr. |
| backup         | no   | no     | yes/no | 備份遠端主機上的文件，在copy之前如果發生什麼意外，原始檔依然能用                                                                                                                                                       |
| content        | no   |        |        | 用來替代src，用於將指定文件的內容，copy到遠端文件內，遠端檔案可不存在，但路徑必須存在                                                                                                                                  |
| decrypt        | no   | yes    | yes/no | This option controls the autodecryption of source files using vault.                                                                                                                                                   |
| dest           | yes  |        |        | 指定要複製的遠程絕對路徑，如果src是資料夾，dest也必須是，如果dest不存在並且dest是以`/`結尾或是src是資料夾，則會創建dest，如果src以及dest皆為檔案並且dest的父級目錄不存在，則任務失敗                                   |
| directory_mode | no   |        |        | 這個參數只能用於遞歸copy目錄時，設定目錄的模式，這個設定後，只會影響不存在的資料夾，原本存在的不會受影響                                                                                                               |
| follow         | no   | no     | yes/no | 當拷貝的文件夾內有link存在的時候，那麼拷貝過去的也會有link                                                                                                                                                             |
| force          | no   | yes    | yes/no | 默認為yes，當內容與源文件不同時將替換遠程文件。如果是no，則僅當目標不存在時才會傳輸文件                                                                                                                                |
| group          | no   |        |        | 設定遠程目錄或是檔案的群組                                                                                                                                                                                             |
| local_follow   | no   | yes    | yes/no | 是否遵循本地機器中的文件系統鏈接                                                                                                                                                                                       |
| mode           | no   |        |        | 等同於chmod，參數可以為"u+rwx or u=rw,g=r,o=r"                                                                                                                                                                         |
| owner          | no   |        |        | 設定遠程目錄或是檔案的擁有者                                                                                                                                                                                           |
| remote_src     | no   | no     | yes/no | 指定src為遠端主機                                                                                                                                                                                                      |
| selevel        | no   | s0     |        | Level part of the SELinux file context. This is the MLS/MCS attribute, sometimes known as the range. _default feature works as for seuser.                                                                             |
| serole         | no   |        |        | Role part of SELinux file context, _default feature works as for seuser.                                                                                                                                               |
| setype         | no   |        |        | Type part of SELinux file context, _default feature works as for seuser.                                                                                                                                               |
| seuser         | no   |        |        | User part of SELinux file context. Will default to system policy, if applicable. If set to _default, it will use the user portion of the policy if available.                                                          |
| src            | no   |        |        | 指定需要copy的文件或目錄，可絕對路徑也可相對路徑，如果以`/`結尾則不會遞歸複製，只會複製當前資料夾                                                                                                                      |
| unsafe_writes  | no   |        | yes/no | 是否以不安全的方式進行，可能導致數據損壞                                                                                                                                                                               |
| validate       | no   | none   |        | 複製前是否檢驗需要復制目的地的路徑                                                                                                                                                                                     |

## 範例操作
1. cli模式
```shell
ansible host_name -m copy -a "src=/home/myuser/test.txt dest=/etc/test.txt" --ask-pass  -vvv

ansible host_name -m copy -a "content='123' dest=/home/alan/test222" --ask-pass  -vvv

ansible host_name -m copy -a "src=test.sh dest=/root dest=/tmp owner=myuser group=mygroup mode=0644
```

2. playbook格式
```yaml
# 複製時帶資料夾權限
- copy
    src: /home/myuser/test.txt
    dest: /etc/test.txt
    owner: myuser
    group: mygroup
    mode: 0644

# 與上述相同，但mode改用符號表示
- copy
    src: /home/myuser/test.txt
    dest: /etc/test.txt
    owner: myuser
    group: mygroup
    mode: u=rw,g=r,o=r

# 複製內容，並且在複製前備份遠端檔案
- copy:
    content: |
      test123
    dest: /some/path/test.txt
    backup: yes

```
## 參考資料
* [copy - Copies files to remote locations](https://docs.ansible.com/ansible/2.4/copy_module.html)
* [【Ansible学习】- 常用文件操作模块之copy模块](https://www.jianshu.com/p/abcfb5cacd90)
## 相關module
* fetch
