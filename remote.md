> add a remote repository
```bash
$ git remote add orange https://gitee.com/sandalphon/weather_predict.git
```

> show names of remote repository
```bash
$ git remote
orange

$ git remote -v
orange  https://gitee.com/sandalphon/weather_predict.git (fetch)
orange  https://gitee.com/sandalphon/weather_predict.git (push)

# 没有远程仓库
$ git remote
fatal: not a git repository (or any of the parent directories): .git
```