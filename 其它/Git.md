# Git

## 集中式

svn

## 分布式

git

---

清屏 con + l

ll ： 详细列表

git init 

git add .

---

流程

- add
  - 生产=>add=>仓库
  - git add .
- commit
  - 注册

git status

- 查看生产车间的状态

---

.gitignore

- *.txt
- \*\*/*.txt
- !a.txt
- /文件夹名

---

rm

- git rm --cached filename只从版本库删除，本地不删除

---

mv

- mv xxx xxx

---

打印：

​	cat a.php

---

git log

git log -p查看文件变动信息

git log -p -1234235678797654321....

git log --oneline

git log oneline --name-only文件发生变化

git log oneline --name-status

---

第一次放到运输车，从暂存区中撤销：git rm -cached xxx.xxx

第n次放到运输车: git reset HEAD xxx.xxx 撤销

恢复到上一次版本，撤回到上一次提交的内容：

​	git checkout -- xxx.xxx 恢复上一个版本

---

git命令别名  git alias

---

## 分支

- 查看分支

  - git branch 

- 创建分支

  - git branch xxx

  - 创建并移动到新分支：

    ​				 git branch -b xxx.xxx

  - 创建之后要add 然后提交才会有最终效果

- 切换到其它分支

  - git checkout xxx

- 合并分支
  - (切换到主分支)git merge xxx

- 删除分支
  - git branch -d xxx
  - 强制删除(没有合并但要删除)：
    - git branch -D xxx

- 冲突
  - 人为修复=>add=>commit

- 分支管理
  - git branch --merged
    - 显示出来说明和master提交点相同
    - 说白了显示出来的是可以删除了的
  - git branch --no -merged

---

## 一般流程

1. git pull
2. git add .
3. git commit -m 'xxx'
4. git remote add origin (_SSH_)
5. git branch -M main
6.  git push origin main
