





## 2025-01-20

### lsof

```shell
# +D 递归
# -w 排出容器进程

lsof -w +D .|grep -v "DIR"

lsof -w +D .|grep -v "DIR"|awk '{print $NF}'|xargs ls -lh|grep "Jan 16"
```







## 2024-12-27

## tar

exclude 需要使用相对路径:

```shell
# relative path
tar --exclude='project/src/router/uploaded' -zcvf project.tar.gz project	
```

