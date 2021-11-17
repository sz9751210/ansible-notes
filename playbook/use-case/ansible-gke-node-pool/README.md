# 安裝 GKE node pool

## host參數說明
| 變數名稱 | 說明 |
| -------- | ------- |
| machine_type | 建置機器規格 |
| boot_disk_size | 硬碟大小 |
| boot_disk_type | 硬碟類型, 預設為pd-standard |
| num_nodes | 預設開啟節點數量 |
| max_nodes | 使用自動調度資源功能最大數量 |
| mix_nodes | 使用自動調度資源功能最小數量 |
| node_labels | 新增Kubernetes 標籤, node selector使用 |

## 執行方式：
```bash
ansible-playbook -i [host檔案] create_gke_node_pool.yml
```

