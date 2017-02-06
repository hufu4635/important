
#Git操作和问题记录

##1.前言
    1. 每次push代码之前，先从服务器pull代码，保证本地代码是最新的
        git pull origin master --allow-unrelated-histories


##2.Git Tag操作
###2.1 Tag操作流程
```
    1. $ git tag test -m '信息'            创建本地Tag
    2. $ git push origin test              推送本地Tag testone到远程仓库
    3. $ git push origin :refs/tags/test   删除远端的Tag标签
    4. $ git tag -d test                   删除本地的Tag标签
    5. $ git tag           展示本地和远端的Tag列表以你当前的代码版本为基准)
```                

###2.2 其他命令
    命令git push origin --tags可以推送全部未推送过的本地标签;        



###2.3 Tag操作问题记录
    remote: GitLab: You are not allowed to change existing tags on this project
    没有权限操作

    $ git push origin testone
    error: src refspec testone does not match any.
    产生原因:需要先在本地创建Tag再进行推送即可




##3.正常修改代码推送

1. git add test.java                进入到对应的目录,添加修改的文件
2. $ git commit -m 'info'           提交add的文件，并添加注释信息
3. $ git log -n 1 --stat            查看最后一次提交了那些文件  
4. $ git push origin master         把提交的文件推送到远程仓库



###3.1 git pull和push遇到的问题
```
1.$ git push origin master
 ! [rejected]        master -> master (non-fast-forward)
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
原因:本地的代码不是最新的
解决:推送代码前需要先从服务器pull最新的代码，

2.$ git pull origin master --allow-unrelated-histories
    ....
     * branch            master     -> FETCH_HEAD
    error: The following untracked working tree files would be overwritten by merge:
            binary/....apk
    Please move or remove them before you merge.
    Aborting

分析:从服务器pull下的文件和本地的文件合并产生了冲突
解决:$ git clean -d -fx  删除一些没有 git add的文件


3. $ git pull origin master --allow-unrelated-histories
Automatic merge failed; fix conflicts and then commit the result
分析:自动合并失败
解决:1.$ git status   查看那些文件有冲突
     2.$ git reset --hard origin/master     丢弃本地所有的修改
```



##4.Git 版本回溯(使用TortoiseGit操作)

###4.1撤销修改
    1.工作区中右击->TortoiseGit->show log
    2.选中对应的版本节点->右击Reset "master" to this...
    3.Reset Type
        soft
        mixed(默认)
        hard 可以让出现黄色或者红色冲突的问题变成绿色(具体原因待续)                        





  