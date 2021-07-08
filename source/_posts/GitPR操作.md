



# pull request的含义

pull request是一项属于GitHub的操作，简单地可以解释为合并请求。

> 用类比的方法来解释一下 pull reqeust。想想我们中学考试，老师改卷的场景吧。你做的试卷就像仓库，你的试卷肯定会有很多错误，就相当于程序里的 bug。老师把你的试卷拿过来，相当于先 fork。在你的卷子上做一些修改批注，相当于 git commit。最后把改好的试卷给你，相当于发 pull request，你拿到试卷重新改正错误，相当于 merge。

当你想与伙伴一同协作开发代码时，你需要用到pull request。

# 实现步骤

小林和小朱要一起开发一个项目。小林作为项目发起者，在GitHub上创建了一个Repository并push了代码。小朱要怎么做呢？

## folk仓库

小朱folk了小林的Repository到自己的仓库，并且Clone已经在**自己仓库中的代码**到本地。

```bash
$ git clone git@github.com:DestinyZjy/SteveLinyz.github.io.git
```

## 查看当前链接情况

小林使用命令查看了小林本地的Repository与哪些远程仓库建立了链接，发现只与自己的Githubd的Repository建立链接。

```bash
$ git remote -v
```

![image-20210630200816105](https://gitee.com/steve-lin08/image-host/raw/master/20210630200816.png)

## 与小朱在Github上的Repository建立链接

现在使用命令来与小朱的Repository建立链接：

```bash
git remote add upstrean https://github.com/DestinyZjy/SteveLinyz.github.io
```

![image-20210630201129537](https://gitee.com/steve-lin08/image-host/raw/master/20210630201129.png)

## 对代码进行修改

### 新建分支

使用命令来新建一个分支，并切换到此分支

```bash
git checkout -b ZJY
```

### 修改代码

小朱对着电脑码了一下午代码，终于完成了小林爸爸的需求。

### 提交

通过命令，小朱在terminal完成了代码的推送，到了自己Github的Repository

```bash
git add xxx
git commit -m "xxx"
git push origin ZJY
```

## 发起Pull Request

小朱到Github上自己的Repository，点击Pull request - New pull request。

![](https://gitee.com/steve-lin08/image-host/raw/master/20210630201924.png)

她选择把ZJY分支的代码提交到小林Repository中的xiaozhu分支，她写下：球球你了帅哥。并且发送了合并请求。

## 同意Merge请求

小林看到了小朱的合并请求，他查看了代码，十分满意，便同意了请求。

结果就是：小林的Repository中的xiaozhu分支，与小朱的ZJY分支完成了合并，小朱成功完成了她的任务！