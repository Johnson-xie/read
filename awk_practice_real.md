



## 2024-12-26

```shell
➜  step1-log head -n2 xxx1_not_enough.log
[2024-12-23 02:05:47,336][Thread-11] INFO task_run(idip_run.py:401) x1,id1,2,0
[2024-12-23 02:05:47,337][Thread-9] INFO task_run(idip_run.py:401) x2,id2,2,0

# delete skin chest not enough
➜  step1-log cat `ls *_not_enough.log`|grep xxxx1|awk -F, '{sum += $NF} END {print sum}'
111
# expected number of deleting skin chest
➜  step1-log cat `ls *_not_enough.log`|grep xxxx2|awk -F, '{sum += $(NF-1)} END {print sum}'
1111

# 1082


# deleted skin
cd step2-log

➜  step2-log ls *_success.log|grep -v task
20241223023555_success.log
20241223024918_success.log
20241223031215_success.log
20241223031510_success.log
20241223031606_success.log

➜  step2-log cat `ls *_success.log|grep -v task`|egrep -v "xx1|xx2|xx3|xx4|xx5|xx6"|wc -l
   35729
```

