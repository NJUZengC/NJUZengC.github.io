---
title: 如何备份Hexo博客
date: 2019-10-14 12:50:29
tags:
    - hexo
    - 博客
categories:
    - hexo使用
---


使用Hexo + GitHub搭建博客，在username.github.io仓库下存储的仅是public文件夹下的静态文件，那我们得如何才能保存hexo的一些具体配置文件呢？在需要更换配置主机时显得尤为重要。在此，根据网络搜索及个人实践，将一些基本步骤记录下来。

## 前期准备
前提需要已经创建好username.github.io仓库，在此需要注意的是在主配置文件<font color='red'>_config.yml</font>已经配置好分支属性为master，如下所示
<br>
```linux
deploy:
  type: git
  repo: https://github.com/{username}/{username}.github.io.git
  branch: master
```
以上 username 是指具体对应的用户名

## 备份
1. 在github上新建分支，不妨称为 save 分支
2. 将 save 分支作为默认分支
3. 将创建的username.github.io仓库clone至本地新文件夹中，并将原先Hexo配置文件夹中的<font color='red'>_config.yml</font>，<font color='red'>themes/</font>，<font color='red'>source/</font>，<font color='red'>scaffolds/</font>，<font color='red'>package.json</font>，<font color='red'>.gitignore</font>复制到username.github.io文件夹中
4. 将themes/{theme_name}/(theme_name指代具体使用的主题名称)中的.git/删除
5. 此时使用git branch命令将显示save分支,表示当前正处于该分支下
```linux
$ git branch
 * save
```
6. 在username.github.io文件夹执行npm命令
```linux
npm install
npm install hexo-deployer-git
```
7. 执行完成后可以看到username.github.io文件夹保留的是此前<font color='red'>public/</font>中的内容，为去除冗余，可以将文件夹下的<font color='red'>2019/</font>，<font color='red'>archives/</font>，<font color='red'>fonts/</font>，<font color='red'>js/</font>，<font color='red'>content.json</font>，<font color='red'>index.html</font>，<font color='red'>search.xml /</font>，<font color='red'>style.css</font>进行删除，由此master分支下与save分支下保持相对清爽
8. 使用git命令将以上修改进行提交
```linux
git status
git add .
git commit -m "备份hexo博客"
git push
```
9. 使用hexo g -d进行生成静态文件部署至Github上。

## 修改
1. 利用hexo命令新建博文
```linux
hexo new "新的博文"
```
2. 在<font color='red'>source/_posts</font>文件夹下修改对应MarkDown文件
3. 执行此前git命令提交hexo网站源文件
4. 执行hexo g -d部署到master分支下

## 参考
[参考资料](https://www.jianshu.com/p/57b5a384f234)
