#git 使用教程
---

## remote link 修改
---
1. git remote -v 查看当前的repo link
2. git remote rm <origin/upstream>   删除remote link
3. git remote add <origin/upstream> <origin/upstream link> 添加remote link

## pull 代码
---
1. git pull -r origin master / git pull -r upstream master

## push 代码
---
1. git push origin master 
 ** 如果需要强制提交 git push origin master -f
 
## 解决conflicts
---
1. 在本地，解决冲突代码
2. git add .  -p 将需要添加的代码add到本地代码库
3. git rebase --continue  #解决完冲突，并且合并到master分支
4. git rebase --abort 取消解决冲突

## 修改commits记录
1. git rebase -i HEAD~<N> 列出需要解决的所有commits 
2. 修改需要处理的commits前面的pick
    r: 修改注释
    d: 删除提交
    s: 合并到前面的提交
    
## Pull request 的使用
1. 首先在提交代码到origin之前， 解决本地代码与upstream代码的冲突。
    git pull -r upstream master
    
2. 处理完冲突之后， 提交代码到origin的master分支
    git push origin master
 
3. 在页面上，创建 pull request 








