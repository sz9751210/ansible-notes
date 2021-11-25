```shell
.
├── README.md
├── create_vm_instance.yaml             # 副本，主要定義role的流程
├── files                               # role會需要複製的檔案
│   ├── instance                        # 存放node_exporter相關檔案
│   │   └── node_exporter
│   │       ├── node_exporter
│   │       └── node_exporter.service
│   └── redis                           # 存放redis以及redis_exporter相關檔案
│       ├── bin
│       │   ├── redis-cli
│       │   ├── redis-server
│       │   └── redis-trib.rb
│       ├── conf
│       │   ├── redis.conf.cluster
│       │   ├── redis.conf.ms
│       │   └── redis.service
│       └── redis_exporter
│           ├── redis_exporter
│           └── redis_exporter.service
├── group_vars                         # 放roles會用到的共同變數
│   └── all
│       ├── env.yml                
│       └── package.yml               
├── inventory.vm.create.yml            # 要安裝的機器host資訊
├── roles                              # roles裡放tasks
│   ├── instance                       # 建立機器的任務 
│   │   └── tasks
│   │       ├── create.yml             # 依照inventory以及vars/instance/instance_var.yml建立instance，可透過group_vars設定是否要byimage建立
│   │       └── setup.yml              # instance的初始化設定以及一些相依套件的安裝，group_vars/all/package.yml可查看相依套件清單
│   ├── monitor                        # 建立prometheus用戶以及node跟redis的exporter
│   │   └── task
│   │       ├── main.yml               # 依照vars/monitor的monitor_var.yml設定task，主要為建立user以及安裝exporter
│   │       ├── node.yml               # 複製node exporter以及相關設定檔並啟動exporter以及設定開機自啟，最後檢查服務是否正常
│   │       └── redis.yml              # 複製redis exporter以及相關設定檔並啟動exporter以及設定開機自啟，最後檢查服務是否正常
│   ├── ops_agent                      # 安裝ops agent，對於監控方便觀察單台的mem disk等狀況
│   │   └── task
│   │       └── main.yml
│   └── redis
│       └── task
│           ├── install_redis.yml      # 複製redis以及相關設定檔並建立log資料夾，調整THP避免效能以及記憶體鎖的問題，並啟動redis
│           ├── main.yml               # 依照vars/redis的redis_var.yml設定task，主要為安裝redis，決定cluster或是M/S mode
│           ├── setup_cluster_role.yml # 確認redis服務是否正常，接著使用redis-cli建立cluster並確認cluster是否正常
│           └── setup_ms_role.yml      # 確認redis服務是否正常，接著使用redis-cli建立slave
└── vars                               # 存放每個roles會用到的變數
    ├── instance                       # 主要放一些建立instance的環境變數以及硬體規格還有網路配置等相關設定
    │   └── instance_var.yml
    ├── monitor                        # 主要設定要安裝的exporter
    │   └── monitor_var.yml
    └── redis                          # 主要設定redis mode，有單台，主從，叢集等選項可配置
        └── redis_var.yml
```

ansible-playbook -i inventory.vm.create.yml create_vm_instance.yaml