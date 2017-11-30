# git-flow

#### 两个主分支：

* master ：只能用来包括产品代码，不能直接工作在这个分支，也不能直接将改动后的代码提交到这个分支上；

* develop：进行任何新的开发的基础分支，当开始一个新的功能分支时，它讲是开发的基础。另外，该分支也汇集所有已完成的功能，并等待被整合到master分支中。

#### 三个辅助分支：

* feature(基于develop)：为即将发布的版本开发新功能特性，完成后merge回develop；

* release(基于develop)：准备要发布版本的分支，用来修复bug，完成后merge回develop和master；

* hotfix(基于master)：修复master上的问题，等不及release版本就必须马上上线，基于master，完成后merge回master和develop。

#### 命令

* git flow init 
  初始化

* git tag -a v0.0.1 -m “标记v1.0版本”
  给master打上tag

* feature
  为即将发布的版本开发新功能，基于develop

* git flow feature start add_feature
  开发新特性，这个分支基于develop，创建add_feature分支，并切换到这个分支下。后面的add_feature自己取，但是最好取得有意义，比如你要完成地图功能map_feature

* git flow feature finish add_feature
  完成开发新特性，会自动合并add_feature分支到develop，然后删除add_feature分支，最后切回到develop分支

* git flow feature publish add_feature
  如果是团队开发，你想把新特性分支发布到远程服务器让其他组员使用，所以使用这命令

* git flow feature pull add_feature
  取得其他用户发布的新特性分支

* release
  准备要发布的分支，用来修复bug，基于develop

* git flow release start v0.1.0
  从develop分支创建一个release分支

* git flow release publish v0.1.0
  提交修改后的代码，供其他组员使用

* git flow release track v0.1.0
  签出release版本的远程变更

* git flow release finish v0.1.0

* git push origin --tags 
  把tag推送到远程仓库，完成release版本，自动执行了：
  1. 归并release分支到master；
  2. 用release分支名打tag；
  3. 归并release分支到develop；
  4. 移除release分支

#### hotfix:紧急修复bug的分支，基于master

* git flow hotfix start v0.0.3
  创建紧急修复的分支

* git flow hotfix finish v0.0.3
  完成了紧急修复，代码归并回develop和master分支，相应的，mater分支打上修正版本的tag创建本地或者远程仓库

      // 初始化一个空的仓库
      git init --bare gitflow.git
      程序员A

      // 复制仓库
      git clone ~/Desktop/gitflow/gitflow.git

      // 初始化git-flow
      git flow init

      // 当前所在分支会切换到了develop
      // 创建一个release分支，用来修复bug
      git flow release start v1.0.1

      // 添加一个文件
      touch a.c
      echo add new file > a.c
      git add .
      git commit -m "add a file"

      // 合并分支
      git flow release finish v1.0.1

      // push到仓库
      git push origin master
