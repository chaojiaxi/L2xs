## github 提交代码



```

# 通过命令把这个目录变成git可以管理的仓库
git init

# 关联到远程库，这里的远程仓库选择Clone with HTTPS的地址。
git remote add origin https://github.com/chaojiaxi/git-pull.git

# 把文件添加到版本库中，添加到暂存区里面去，不要忘记后面的小数点“.”，意为添加文件夹下的所有文件
git add .

# 告诉Git，把文件提交到本地仓库。引号内为提交说明
git commit -m 'creat project'

# 拉取文件合并冲突
git pull https://github.com/chaojiaxi/git-pull.gitt master

# 本地库的内容推送到远程
git push origin master

```

