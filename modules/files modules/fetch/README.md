# fetch

- 用途：將遠端主機上的文件拉取到ansible本機

## 選項

| 參數              | 必要 | 預設值 | 選項   | 說明                                                                                                                                                           |
| ----------------- | ---- | ------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dest              | yes  |        |        | 指定要複製回本機上的路徑，如果dest是以/backup而src的檔案叫做/etc/profile並且主機名叫host.example.com，則複製回來的路徑會是/backup/host.example.com/etc/profile |
| fail_on_missing   | no   | no     | yes/no | 當設置為`yes`時，如果由於任何原因無法讀取遠程文件，則任務將失敗                                                                                                |
| flat              | no   |        |        | Allows you to override the default behavior of appending hostname/path/to/file to the destination. 直接將檔案複製到資料夾內                                                             |
| src               | yes  |        |        | 指定遠端要複製的目錄或文件位置                                                                                                                                 |
| validate_checksum | no   | yes    | yes/no | Verify that the source and destination checksums match after the files are fetched.                                                                            |

## 範例操作
1. cli格式
```shell
ansible host_name -m fetch -a "src=/etc/fstab dest=/testdir/ansible"
```

2. playbook格式
```yaml
# 將遠端的檔案放到/tmp/fetched/host.example.com/tmp/somefile
- fetch:
    src: /tmp/somefile
    dest: /tmp/fetched

# Specifying a path directly
- fetch:
    src: /tmp/somefile
    dest: /tmp/prefix-{{ inventory_hostname }}
    flat: yes

# 複製回本機的路徑為/tmp/special/uniquefile
- fetch:
    src: /tmp/uniquefile
    dest: /tmp/special/
    flat: yes

# Storing in a path relative to the playbook
- fetch:
    src: /tmp/uniquefile
    dest: special/prefix-{{ inventory_hostname }}
    flat: yes
```

## 參考資料
* [fetch - Fetches a file from remote nodes — Ansible Documentation](https://docs.ansible.com/ansible/2.4/fetch_module.html)
* [ansible模块fetch_安然。。的博客-程序员宅基地_ansible fetch - 程序员宅基地 (cxyzjd.com)](https://www.cxyzjd.com/article/weixin_44791884/105024589)
## 相關module
* copy
