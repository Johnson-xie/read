

## 2024-12-27

### awk

```shell
[root@VM-0-16-centos awk-test]# cat items-sold.txt
101 2 10 5 8 10 12
102 0 1 4 3 0 2
103 10 6 11 20 5 13
104 2 3 4 0 6 5
105 10 2 5 7 12 6
[root@VM-0-16-centos awk-test]# cat items-sold.txt |awk 'BEGIN {sum=0} {sum+=$1} END{print sum}'
515
[root@VM-0-16-centos awk-test]# cat items-sold.txt |awk 'BEGIN {sum=0} {sum+=$NF} END{print sum}'
38
```





### leetcode shell

```shell
cat file.txt|egrep '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$|^[0-9]{3}-[0-9]{3}-[0-9]{4}$'

egrep '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$|^[0-9]{3}-[0-9]{3}-[0-9]{4}$' file.txt

# match num
head all_delete_data.csv|awk -F, '{sum += $3} END {print sum}'
head all_delete_data.csv|awk -F, '{print $3}'|sed -n '/[07]/p'

# group regex
egrep '^(\([0-9]{3}\) |[0-9]{3}-)[0-9]{3}-[0-9]{4}$' file.txt

# multiple regex
grep -e "^[0-9]\{3\}\-[0-9]\{3\}\-[0-9]\{4\}$" -e "^([0-9]\{3\}) [0-9]\{3\}\-[0-9]\{4\}$" file.txt


# print 10th line
sed -n '10 p' file.txt
sed -n 10p file.txt
awk 'NR == 10' file.txt
sed '10q;d' file.txt
# ; multiple commands
sed 's/foo/bar/; s/baz/qux/' inputfile


# sort
cat words.txt|tr -s ' '|tr ' ' '\n'|grep -v '^$'|sort|uniq -c|awk '{print $2,$1}'|sort -nrk2
# tr -s 2 parameters
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -r | awk '{ print $2, $1 }'

# transpose file
# no pass
l1=()
l2=()
while IFS= read -r i
do
    l1+=`echo $i|awk '{print $1}'`
    l2+=`echo $i|awk '{print $2}'`
done < file.txt
echo $l1
echo $l2

➜  origin_data git:(main) ✗ seq 1 5                                                                                                                              git:(main|●3✚1…38⚑1
1
2
3
4
5
```

