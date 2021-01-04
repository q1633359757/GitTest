1、下载安装Git https://git-scm.com/downloads

2、打开Git Bash 配置全局属性。
	git config --global user.email "qfxsxhfy@126.com"
	git config --global user.name "navyzhou"

3、生成密钥
	ssh-keygen -t rsa -C "qfxsxhfy@126.com"
	第一次会提醒你是否需要修改密钥文件的保存路径，按回车使用默认路径就行
	接下来会提醒你输入两次密码，这个密码要记住，到时候远程访问时候需要用到

4、将密钥配置到你的GitHub账号中，先登录GitHub账号 -> Settings -> SSH and GPG keys -> New SSH key 
	将刚才生成的密钥文件id_rsa.pub中的内容拷贝到Key文本框中

5、创建本地仓库
	先在本地创建一个空目录，用来存到你的项目代码。
	比如：如果我想把本地仓库放在D盘，那么在D盘右击 -> Git Bash Here 在当前路径打开。在D盘创建一个空目录，我的是fresh。
		通过指令：mkdir fresh 创建
	这个时候可以把你要交给git管理的项目拷贝到这个目录中，你也可以就用以前的工作区间里面的项目。
	
6、通过git init把这个文件夹变成git可管理的仓库。注意，该指令需要在项目文件夹下运行。
	成功后，会在项目文件夹下出现一个.git的目录

7、可以通过指令git status来查看当前的状态，你会发现很多文件没有加到仓库
	将我们的项目代码添加到仓库中，通过git add . 可以将所有代码添加到本地仓库
	
8、将代码提交到本地仓库
	git commit -m "初始导入"
	
9、把本次仓库中的代码提交到远程仓库
	首先我们必须在远程Github中创建一个仓库，创建好之后会有一个https://github.com/navyzhou/fresh.git
	
10、将Github上创建好的Git仓库跟本地仓库关联
	git remote add origin https://github.com/navyzhou/fresh.git
	
11、关联好之后，我们将本地仓库代码提交到远程仓库
	git push -u origin  master。 注意：第一次提交的时候远程仓库是空的，所以我们需要加-u，等远程仓库有内容了，下次提交修改代码时不需要-u参数

12、从远程服务器克隆下来
	git clone git@218.196.14.100:/home/git/yc_javaee_8_1.git D:/yc
	
13、远程服务器更新到本地：git pull origin master
	
	git rm -r --cached .
14、添加文件到仓库: git add .
 
15、提交文件到仓库：git commit -m '初始化项目版本'
 
16、提交到远程仓库：git push origin master
 
17、显示提交的信息：git log

18、列出所有本地分支 ：git branch

1 9、列出所有远程分支：git branch -r

20、列出所有本地分支和远程分支：git branch -a

21、新建一个分支，但依然停留在当前分支：git branch [branch-name]

22、新建一个分支，并切换到该分支：git checkout -b [branch] 

23、切换到指定分支，并更新工作区：git checkout [branch-name] 

24、合并指定分支到当前分支：git merge [branch] 

25、删除分支：git branch -d [branch-name]

26、删除远程分支 ：git push origin --delete [branch-name]  git branch -dr [remote/branch]

27、多密钥管理
    先生成密钥，注意需要修改密钥文件名称。然后将新密钥加载到SSH agent中
    执行：ssh-agent bash --login -i
	      ssh-add <要添加的密钥>
     注意：以后每次提交都需要进行这两步 

冲突：
	如果希望保存本地改动并拉下最新服务器代码，手动merge
		git stash  保留服务器上的修改
		git stash list   将当前的Git栈信息打印出来,stash@{0}就是刚才保存的标记
		git pull   暂存了本地修改之后，pull内容
		git stash pop stash@{0}   还原暂存的内容,系统自动合并修改的内容，但是其中有冲突，需要解决其中的冲突
		打开冲突的文件,解决文件中冲突的的部分
		git stash drop stash@{0}  删除stash 清除0编号的stash
		git  stash clear  清除所有stash
	
	如果希望服务器上版本完全覆盖本地修改，使用如下命令回退并更新
		git reset --hard  放弃本地修改
		git pull