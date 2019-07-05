# git

工作中先克隆下来,在将自己的代码拷贝到克隆的文件夹中,然后执行add commit 最后push上传文件

```
git clone https://gitee.com/errlei/testmayun.git
git add --all
git commit -m '添加了一个加密功能'
git push https://gitee.com/errlei/testmayun.git master
// 如果push失败，证明你和远程的版本不一致，先git pull拉取一下远程代码，手动解决了冲突之后再提交 git push
git status
git log --oneline
```



> 在自己创建的分支中操作修改完成功能之后在dev中合并自己的代码
创建git
```
git init
```

## 一. 配置用户名邮箱

```
git config --global user.name ""
git config --global user.email ""
```

## 二. 上传到暂存区

git add 文件夹/文件名

### 全部上传

git add --all

## 三. 添加到当前版本管理库

git commit -m '注释内容'

## 查看当前仓库图形界面

gitk

## 查看当前文件状态

git status

## 查看提交的版本号

git reflog 

## 将文件上传服务器(GitHub)

git push 地址 master

## 更新

git pull ''/地址

## 克隆

git clone 地址

## 忽略文件

> .gitignore文件中写入

这个文件表示 被忽略的文件的路径或者文件名
一般的写法是
/.idea    // 会忽略.idea文件
/js       // 会忽略js目录下面所有的文件
/js/*.js  // 会忽略js目录下面所有后缀名为js的文件
/.gitignore // 忽略自己
/node_modules  // 一般这个文件夹是不用上传到仓库里面的，所以会忽略掉
这个在git add的时候就不会给你提交上去
git status的时候 也看不到忽略的文件夹或文件

## 回退

git reset --hard Head
git reset --hard Head~0   //使用 git reflog查看有几个Head

##### git reset --hard 版本号  // 直接回退到某个版本号 (常用)

## 分支

1. ##### 查看分支
	
	git branch // 查看本地分支
		git branch -a // 查看所有分支  -r是查看远程分支
2. ##### 创建分支
	
		git branch dev
3. ##### 切换分支
	
	git checkout dev
		git checkout master
4. ##### 合并分支
	
		git merge dev --no-ff  // 加上参数能看到曾经的合并历史
5. 删除分支
		git branch -d dev //一般开发是合并到主分支没什么问题后，就删除分支

> 每天我们上班的工作第一件事不是写代码，而是使用git pull命令，同步仓库的代码，也许昨天公司其他同事向仓库里面push了代码，你就要先拉取，再写你自己的代码，不然后面就会有冲突
>