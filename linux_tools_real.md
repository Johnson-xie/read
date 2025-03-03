





## 2025-03-03



### json to yaml

```shell
➜  test echo '
{
  "volumes": [
    {
      "name": "lsgame-node",
      "hostPath": {
        "path": "/data/home/user00/lsgame-docker",
        "type": "DirectoryOrCreate"
      }
    },
    {
      "name": "corefile-node",
      "hostPath": {
        "path": "/data/corefile",
        "type": "DirectoryOrCreate"
      }
    }
  ]
}'|yq -P

volumes:
  - name: lsgame-node
    hostPath:
      path: /data/home/user00/lsgame-docker
      type: DirectoryOrCreate
  - name: corefile-node
    hostPath:
      path: /data/corefile
      type: DirectoryOrCreate
➜  test
```





### yaml to json

```shell
➜  test echo '
name: John Doe
age: 30
skills:
  - Python
  - Bash
  - jq'|yq -o json
{
  "name": "John Doe",
  "age": 30,
  "skills": [
    "Python",
    "Bash",
    "jq"
  ]
}
```









## 2025-02-20

merge kubeconfigs

```shell
[root@ip-172-24-2-43 qiangxie]# cat sync_credentail.sh
#!/bin/bash

SOURCE="/root/.kube"
TMP_DIR=~/.k9s_tmp
TENCENT_ACCOUNT=123456789

set -x

[ ! -d $TMP_DIR ] && mkdir $TMP_DIR

cd $SOURCE
rsync -av --include="ingame-*"  --exclude=* ./ $TMP_DIR

cd $TMP_DIR
ls -ltrh

for i in `ls -l|sort -k9|grep ingame-|awk '{print $NF}'|tr '\n' " "`
do
	suffix=`echo $i|awk '{print $NF}'|awk -F"-" 'BEGIN{OFS="-"} {print $2,$3}'`
	echo $i $suffix
  # sed -i -e "s/cls-\([a-zA-Z0-9]\{8\}\)-$TENCENT_ACCOUNT-context-default/${suffix}-\1/g" $i
  sed -i "/cls-\([a-zA-Z0-9]\{8\}\)-$TENCENT_ACCOUNT-context-default/ s/cls/$suffix/g" $i
	# test
	# export KUBECONFIG=$i
	# timeout 5 kubectl get ns
done

CMD=`ls -l|sort -k9|grep ingame-|awk '{print $NF}'|tr '\n' ":"`
CMD="KUBECONFIG=${CMD%%:} kubectl config view --merge --flatten > ~/.kube/config"


echo $CMD
eval $CMD


rm -rf $TMP_DIR
```





## 2025-02-12

### top

```shell
top -p {pid}

# send signal, default 15
k -> pid -> enter; enter

# sort
M
P
T

# save settings
W

top -u {username}
# adjust display unit
E
e

# 查看每个cpu的使用情况
1
# 图形化展示
t
```





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

