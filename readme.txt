clear清理
exit 退出


创建版本库
git init


--在本机上创建用户吧？
git config --global user.name "luzhijie";
git config --global user.email "364460369@qq.com"


git add   filename
git commit -m "add distributed"



git status	要随时掌握工作区的状态

git diff filename 查看被修改文件的修改内容 

查看操作文件版本记录(中是简单信息)
git log (--pretty=oneline)

版本跳转退回上一版本
git reset --hard HEAD^
git reset --hard commitid

将工作区(就是你的实时编辑)的文件丢弃---相当于从版本库中提取了一个新的替换到了工作区可以解决误删问题
git checkout -- readme.txt
将暂存区(就是你add的)的文件丢回工作区
git reset HEAD readme.txt

删除文件
git rm test.txt
再提交git commit



创建秘钥
ssh-keygen -t rsa -C "364460369@qq.com"


从命令行推送已经创建的仓库
git remote add origin allview@172.16.248.4:luzhijie/mygit.git
git remote add origin https://github.com/luzhij828/mytest.git



获取远程库与本地同步合并（如果远程库不为空必须做这一步，否则后面的提交会失败）
git pull --rebase origin master
将修改完的文件，add之后git rebase --continue

删除远程仓库
git remote rm origin

第一次提交同步
git push -u origin master
之后提交origin是远程库的默认名，master是本地版本库主分支
git push origin master

克隆远程仓库
git clone allview@172.16.248.4:luzhijie/mygit.git


创建分支dev
git checkout -b dev
使用-b表示创建并切换，相当于
git branch dev  --创建
git checkout dev    --切换
查看当前分支和所有分支
git branch 

切回master
git checkout master
将dev合并进入当前所在分支
git merge dev
删除dev分支
git branch -d dev
查看分支合并图
git log --graph      带参数
git log --graph --pretty=oneline --abbrev-commit		不带参数
当合并是发生文件内容冲突时，会提示让人手工进行修改，并且冲突的地方会进行标注·
之后再进行add commit 提交

在合并分支时保留被合并分支的版本信息使用--no-ff参数，相当于一个再次提交
git merge --no-ff -m "merge with no-ff" dev


将当前工作区暂时封存储，git status 将没有之前的改动状态（估计就是为了这点吧）想可以优先执行在其他分支上进行其他操作
git stash
查看当前分支所有的暂时封存
git stash list
恢复指定的封存
git stash apply stash@{0}	提取
git stash drop stash@{0}	删除
git stash pop stash@{0}		提取并删除

对于一个还没有合并的分支，想要删除必须强制删除
git branch -D fengzhiNAME




多人协作模式，多人使用同一个远程库
git remote -v	查看远程库信息
在本地创建的其他分支如果不推送到远程库，其他人克隆下来的版本库是看不见这些分支的
git clone allview@172.16.248.4:luzhijie/mygit.git
git checkout -b dev origin/dev		如果要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支
然后可以进行在dev分支上的操作并且提交，当其他用户也在操作提交该远程库的相同分支的文件时，提交时报错
需要git pull 将远程库中的改变抓取回本地，如果还报错，则将本地dev分支和远程库分支dev进行关联
git branch --set-upstream dev origin/dev
之后再进行git pull ，会标记出来被修改的文件，去进行修改在add、 commit、提交远程库git push origin dev
