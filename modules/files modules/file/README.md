# file

- 用途：設置文件屬性

## 選項

| 參數          | 必要 | 預設值 | 選項                                  | 說明                                                                                                                                                                                                                                                                                                             |
| ------------- | ---- | ------ | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| attribute     | no   | none   |                                       | Attributes the file or directory should have. This string should contain the attributes in the same order as the one displayed by lsattr.                                                                                                                                                                        |
| follow        | no   | no     | yes/no                                | This flag indicates that filesystem links, if they exist, should be followed.                                                                                                                                                                                                                                    |
| force         | no   | no     | yes/no                                | 需要在兩種情況下強制創建軟鏈接，一種是源文件不存在但之後會建立的情況下；另一種是目標軟鏈接已存在,需要先取消之前的軟鏈，然後創建新的軟鏈                                                                                                                                                                          |
| group         | no   |        |                                       | 定義文件/目錄的群組                                                                                                                                                                                                                                                                                              |
| mode          | no   |        |                                       | 定義文件/目錄的權限                                                                                                                                                                                                                                                                                              |
| owner         | no   |        |                                       | 定義文件/目錄的擁有者                                                                                                                                                                                                                                                                                            |
| path          | yes  |        |                                       | 定義文件/目錄的路徑                                                                                                                                                                                                                                                                                              |
| recurse       | no   | no     | yes/no                                | 遞歸的設置文件的屬性，只對目錄有效                                                                                                                                                                                                                                                                               |
| selevel       | no   | s0     |                                       | Level part of the SELinux file context. This is the MLS/MCS attribute, sometimes known as the range. _default feature works as for seuser.                                                                                                                                                                       |
| serole        | no   |        |                                       | Role part of SELinux file context, _default feature works as for seuser.                                                                                                                                                                                                                                         |
| setype        | no   |        |                                       | Type part of SELinux file context, _default feature works as for seuser.                                                                                                                                                                                                                                         |
| seuser        | no   |        |                                       | User part of SELinux file context. Will default to system policy, if applicable. If set to _default, it will use the user portion of the policy if available.                                                                                                                                                    |
| src           | no   |        |                                       | 要被連結到的源文件路徑，只適用於state=link的情況                                                                                                                                                                                                                                                                 |
| state         | no   | file   | file/link/directory/hard/touch/absent | 底下說明                                                                                                                                                                                                                                                                                                         |
| unsafe_writes | no   |        | yes/no                                | Normally this module uses atomic operations to prevent data corruption or inconsistent reads from the target files, sometimes systems are configured or just broken in ways that prevent this. One example are docker mounted files, they cannot be updated atomically and can only be done in an unsafe manner. |

## 範例操作
```yaml
# 修改/etc/foo.conf的屬性
- file:
    path: /etc/foo.conf
    owner: foo
    group: foo
    mode: 0644
- file:
    src: /file/to/link/to
    dest: /path/to/symlink
    owner: foo
    group: foo
    state: link

# 遞歸變更資料夾目錄權限
- file:
    path: /etc/foo
    state: directory
    recurse: yes
    owner: foo
    group: foo

# 透過touch建立檔案並設定權限
- file:
    path: /etc/foo.conf
    state: touch
    mode: "u=rw,g=r,o=r"

# 與上述相同，僅修改設置權限表達式
- file:
    path: /etc/foo.conf
    state: touch
    mode: "u+rw,g-wx,o-rwx"

# 建立目錄
- file:
    path: /etc/some_directory
    state: directory
    mode: 0755

# 遞歸刪除
- file:
    path: /etc/foo
    state: absent
```


>state說明
>* directory：如果目錄不存在，創建目錄
>* file：即使文件不存在，也不會被創建
>* link：創建軟鏈接
>* hard：創建硬鏈接
>* touch：如果文件不存在，則會創建一個新的文件，如果文件或目錄已存在，則更新其最後修改時間
>* absent：刪除目錄、文件或者取消鏈接文件


## 參考資料
* [file - Sets attributes of files — Ansible Documentation](https://docs.ansible.com/ansible/2.4/file_module.html)
* [ansible之file模块 - 简书 (jianshu.com)](https://www.jianshu.com/p/61da905b457f)