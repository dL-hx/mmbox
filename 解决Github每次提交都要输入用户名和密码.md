方法一
执行如下代码

git remote -v          # 查看远程库名称

不出意外的话，可以看到

origin	https://github.com/你的用户名/你的仓库名.git (fetch)
origin	https://github.com/你的用户名/你的仓库名.git (push

接下来需要改掉 https 连接协议

git remote rm origin      # 删除名为 `origin` 的远程库
git remote add origin git@github.com:你的用户名/你的仓库名.git

方法二
不需要删掉远程库，直接修改本地的 .git/config 文件，用记事本打开，你会看到

[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = https://github.com/你的用户名/你的仓库名.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master


注意第 9 行，是 https 协议，接下来只需要向上面一样改掉他：

url = git@github.com:你的用户名/你的仓库名.git
