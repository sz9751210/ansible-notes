# ansible-notes

## 架構
```shell
ansible_project
├── files                      # 放roles需要的檔案
├── group_vars                 # 放共同的變數
├── inventory.dev.yml          # 開發環境的主機清單
├── inventory.prod.yml         # 正式環境的主機清單
├── main.yml                   # 劇本檔，定義要用到哪些roles
├── roles                      # 放roles的任務
│   ├── instance               # 定義instance這個role
│   │   └── tasks              # instance的task
│   │       └── main.yml
│   └── monitor                # 定義monitor這個role
│       └── tasks              # monitor的task
│           └── main.yml
└── vars                       # 放roles的變數
    ├── instance
    └── monitor
```

