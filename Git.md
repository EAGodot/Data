
# 免費的github空間為1G
# 獲取git軟件版本
`git --version`

# git配置文件在哪個位置
    https://blog.51cto.com/u_13746169/5876491
    C:/Users/用户名文件夹/.gitconfig 文件中
# 示例
在开始Git之旅之前，我们需要设置一下Git的环境变量，这个设置是一次性的工作。即这些设置会在全局文件（用户主目录下的:file:`.gitconfig`）或系统文件（:file:`/etc/gitconfig`）中做永久的记录
    1. 告诉Git当前用户的姓名和邮件地址，配置的用户名和邮件地址将在版本库提交时作为提交者的用户名和邮件地址。
    	``` 
        $ git config --global user.name "Jiang Xin"
        $ git config --global user.email jiangxin@ossxp.com
	```
    2. 设置一些Git别名，以便可以使用更为简洁的子命令。
        如果拥有系统管理员权限（可以执行:command:`sudo`命令），希望注册的命令别名能够被所有用户使用，可以执行如下命令：
	```  	
	$ sudo git config --system alias.br branch
	$ sudo git config --system alias.ci "commit -s"
	$ sudo git config --system alias.co checkout
	$ sudo git config --system alias.st "-p status"
	```		
20230513：
		gitlab使用記錄tag:1
			設置全局配置
				$ git config --global user.name "Jiang Xin"
				$ git config --global user.email jiangxin@ossxp.com			
			初始化本地代碼文件夾git			
				$ git init
				$ git config  user.name "Jiang Xin"
				$ git config  user.email jiangxin@ossxp.com	
			參考：
				https://blog.csdn.net/VLOKL/article/details/132344964
			切换默认分支
			默认情况下，GitHub 仓库的主分支名称是 "master"，但为了更加包容和尊重的命名，GitHub 已经将默认分支更改为 "main"。您可以通过以下命令将本地仓库的默认分支切换为 "main"：
				git branch -m master main
			創建本地ssh密鑰並配置進gitlab的個人ssh密鑰裏面
				https://blog.csdn.net/chang_chunhua/article/details/130807999
			連接到遠程代碼倉庫
				git remote add origin 远程仓库的地址
				
			获取远程更改
				在开始添加和提交更改之前，确保您的本地仓库是最新的。执行以下命令从远程仓库获取最新的更改：
				git pull origin main				
			如果出现不相关历史的错误提示，您可以使用以下命令来解决：
				git pull origin main --allow-unrelated-histories		
			添加文件到暂存区
				如果您有新的或已修改的文件需要提交，使用以下命令将它们添加到暂存区：
				git add .	
			提交更改
				一旦您的更改被添加到暂存区，执行以下命令来提交更改并添加提交信息：
				git commit -m "Your commit message"
			尝试使用 SSH 协议
			为了增强安全性和便捷性，您可以尝试使用 SSH 协议来推送更改，而不是使用 HTTPS。首先，在 GitHub 上添加您的 SSH 公钥。然后，将远程仓库 URL 更改为 SSH 格式：
				git remote set-url origin git@github.com:SLDragon-cx330/end.git
			上传项目
				最后，使用以下命令将您的项目文件推送到 GitHub 远程仓库：
				git push origin main		
		gitlab使用記錄tag:2
			刪除創建的小組
				https://blog.csdn.net/seven_xu_/article/details/125630052
	
3、創建版本庫
    $ cd /path/to/my/workspace
    $ mkdir demo
    $ cd demo
    $ git init
    初始化空的 Git 版本库于 /path/to/my/workspace/demo/.git/

    隐藏的:file:`.git`目录就是Git版本库（又叫仓库，repository）
    :file:`.git`版本库目录所在的目录，即:file:`/path/to/my/workspace/demo`目录称为 工作区，
    目前工作区除了包含一个隐藏的file:.git版本库目录外空无一物。
    下面为工作区中加点料：在工作区中创建一个文件:file:`welcome.txt`，内容就是一行“ Hello. ”。
    $ echo "Hello." > welcome.txt
    为了将这个新建立的文件添加到版本库，需要执行下面的命令：
    $ git add welcome.txt

    //添加當前目錄下所有文件到暫存區
    git add .


    切记，到这里还没有完。Git和大部分其他版本控制系统都需要再执行一次提交操作，对于Git来说就是执行:command:`git commit`命令完成提交
    $ git ci -m "initialized"
        1、使用了Git命令别名，即:command:`git ci`相当于执行:command:`git commit`。在本节的一开始就进行了Git命令别名的设置。
        2、通过 -m 参数设置提交说明为："initialized"。该提交说明也显示在命令输出的第一行中。
        3、命令输出的第一行还显示了当前处于名为 master 的分支上，提交ID为7e749cc[3]，且该提交是该分支的第一个提交，即根提交（root-commit）。
        根提交和其他提交的区别在于没有关联的父提交，这会在后面的章节中加以讨论。
        4、命令输出的第二行开始显示本次提交所做修改的统计：修改了一个文件，包含一行的插入。
4、思考：为什么工作区下有一个 :file:`.git` 目录？
    $ git grep " 工作区文件内容搜索
    1、当工作区中包含了子目录，在子目录中执行Git命令时，如何定位版本库呢？
        实际上，当在Git工作区目录下执行操作的时候，会对目录依次向上递归查找:file:`.git` 目录，
        找到的:file:`.git`目录就是工作区对应的版本库，:file:`.git`所在的目录就是工作区的根目录，
        文件:file:`.git/index`记录了工作区文件的状态（实际上是暂存区的状态）。
        例如在非Git工作区执行:command:`git`命令，会因为找不到:file:`.git`目录而报错。

        如果跟踪一下执行:command:`git status`命令时的磁盘访问[4]，会看到沿目录依次向上递归的过程。
        $ strace -e 'trace=file' git status

    2、那么有什么办法知道Git版本库的位置，以及工作区的根目录在哪里呢？
        显示版本库:file:`.git`目录所在的位置。
            $ git rev-parse --git-dir
            E:/ecovacs/Gemini/Software_Gemini_Mini_A_V0001/.git

注意：       git rev-parse講解
            git rev-parse是git revision-parse的缩写用于解析和显示Git对象的引用或标识符的值
            https://www.cnblogs.com/lxd670/p/17556140.html


        显示工作区根目录
            $ git rev-parse --show-toplevel
        相对于工作区根目录的相对目录
            $ git rev-parse --show-prefix
        显示从当前目录（cd）后退（up）到工作区的根的深度
            $ git rev-parse --show-cdup
5、思考： :command:`git config` 命令参数的区别？
    在之前出现的:command:`git config`命令，有的使用了 --global 参数，有的使用了 --system 参数，这两个参数有什么区别么？
        执行下面的命令，将打开:file:`/path/to/my/workspace/demo/.git/config`文件进行编辑。
            $ cd /path/to/my/workspace/demo/
            $ git config -e
        执行下面的命令，将打开:file:`/home/jiangxin/.gitconfig`（用户主目录下的:file:`.gitconfig`文件）全局配置文件进行编辑。
            $ git config -e --global
        执行下面的命令，将打开:file:`/etc/gitconfig`系统级配置文件进行编辑。
        如果Git安装在:file:`/usr/local/bin`下，这个系统级的配置文件也可能是在:file:`/usr/local/etc/gitconfig`。
            $ git config -e --system
    Git的三个配置文件分别是版本库级别的配置文件、全局配置文件（用户主目录下）和系统级配置文件（:file:`/etc`目录下）。
    其中版本库级别配置文件的优先级最高，全局配置文件其次，系统级配置文件优先级最低。
    这样的优先级设置就可以让版本库:file:`.git`目录下的:file:`config`文件中的配置可以覆盖用户主目录下的Git环境配置。
    而用户主目录下的配置也可以覆盖系统的Git配置文件。

        Git配置文件采用的是INI文件格式

        command:`git config <section>.<key>`，来读取INI配置文件中某个配置的键值。例
        如读取 [core] 小节的 bare 的属性值，可以用如下命令：
            $ git config core.bare
            false
        如果想更改或设置INI文件中某个属性的值也非常简单，命令格式是：
        :command:`git config <section>.<key> <value>`。可以用如下操作
            $ git config a.b something
            $ git config x.y.z others

        从上面的介绍中，可以看到使用:command:`git config`命令可以非常方便地操作INI文件，
        实际上可以用:command:`git config`命令操作任何其他的INI文件。
            向配置文件:file:`test.ini`中添加配置。
                $ GIT_CONFIG=test.ini git config a.b.c.d "hello, world"
            从配置文件:file:`test.ini`中读取配置。
                $ GIT_CONFIG=test.ini git config a.b.c.d
                hello, world

6、思考：是谁完成的提交？
    执行下面的命令，删除Git全局配置文件中关于 user.name 和 user.email 的设置：
        $ git config --unset --global user.name
        $ git config --unset --global user.email

        //備注：未完成

7、Git暂存区
    可以用:command:`git log`查看提交日志（附加的 --stat 参数看到每次提交的文件变更统计）
        git log --stat
        git log --pretty=oneline    //看精簡日志

        //查看文件状态，也可以看到文件处于未提交的状态，附加上 -s 参数，显示精简格式的状态输出
        git status -s

            虽然都是 M（Modified）标识，但是位置不一样。在执行:command:`git add`命令之
            前，这个 M 位于第二列（第一列是一个空格），在执行完:command:`git add`之后，字
            符 M 位于第一列（第二列是空白）。
            位于第一列的字符 M 的含义是：版本库中的文件和处于中间状态——提交任务（提交暂
            存区，即stage）中的文件相比有改动。
            位于第二列的字符 M 的含义是：工作区当前的文件和处于中间状态——提交任务（提交
            暂存区，即stage）中的文件相比也有改动

        可以通过执行:command:`git diff`命令看到修改后的文件和版本库中文件的差异。
        （实际上这句话有问题，和本地比较的不是版本库中的文件，而是一个中间状态的文件）
        git diff
        如果和HEAD（当前版本库的头指针）或者master分支（当前工作分支）进行比较，会发现有差异
        git diff HEAD
        通过参数 --cached 或者 --staged 参数调用:command:`git diff`命令，看到的是提交暂存区（提交任务，stage）和版本库中文件的差异。
        git diff --cached


        暫存區的理解：
            工作區-->暫存區--->版本庫
            通過git add將變更提交到暫存區，通過git commit將暫存區的内容更新到版本庫

        文件:file:`.git/index`实际上就是一个包含文件索引的目录树，像是一个虚拟的工作
        区。在这个虚拟工作区的目录树中，记录了文件名、文件的状态信息（时间戳、文件长度
        等）。文件的内容并不存储其中，而是保存在Git对象库:file:`.git/objects`目录中，文
        件索引建立了文件和对象库中对象实体之间的对应。

        图中，可以看到部分Git命令是如何影响工作区和暂存区（stage，亦称index）的。
        下面就对这些命令进行简要的说明，而要彻底揭开这些命令的面纱要在接下来的几个章
        节。
            1、图中左侧为工作区，右侧为版本库。在版本库中标记为 index 的区域是暂存区
            （stage，亦称index），标记为 master 的是master分支所代表的目录树。
            图中可以看出此时HEAD实际是指向master分支的一个“游标”。所以图示的命令中出
            现HEAD的地方可以用master来替换。

            2、图中的objects标识的区域为Git的对象库，实际位于:file:`.git/objects`目录下，
            当对工作区修改（或新增）的文件执行:command:`git add`命令时，暂存区的目录树
            被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。
            当执行提交操作（:command:`git commit`）时，暂存区的目录树写到版本库（对象
            库）中，master分支会做相应的更新。即master最新指向的目录树就是提交时原暂存区的目录树。

            3、当执行:command:`git reset HEAD`命令时，暂存区的目录树会被重写，被master分支
            指向的目录树所替换，但是工作区不受影响。

            4、当执行:command:`git rm --cached <file>`命令时，会直接从暂存区删除文件，工作
            区则不做出改变。

            5、当执行:command:`git checkout .`或者:command:`git checkout -- <file>`命令
            时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作
            区中未添加到暂存区的改动。

            6、当执行:command:`git checkout HEAD .`或者:command:`git checkout HEAD
            <file>`命令时，会用HEAD指向的master分支中的全部或者部分文件替换暂存区和以及
            工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改
            动，也会清除暂存区中未提交的改动。

8、Git Diff魔法
    瀏覽當前版本庫目錄樹
        HEAD（版本库中当前提交）指向的目录树
        $ git ls-tree -l HEAD
        100644 blob fd3c069c1de4f4bc9b15940f490aeb48852f3c42 25 welcome.txt

    暂存区目录树的浏览
        浏览暂存区中的目录树之前，首先清除工作区当中的改动。通过:command:`git clean -
        fd`命令清除当前工作区中没有加入版本库的文件和目录（非跟踪文件和目录），然后执
        行:command:`git checkout .`命令，用暂存区内容刷新工作区
            $ git clean -fd
            $ git checkout .
        要显示暂存区的目录树，可以使用:command:`git ls-files`命令。
        $ git ls-files -s
    兩者區別：
        注意这个输出和之前使用:command:`git ls-tree`命令输出不一样，如果想要使
        用:command:`git ls-tree`命令，需要先将暂存区的目录树写入Git对象库
        （用:command:`git write-tree`命令），然后在针对:command:`git write-tree`命令写
        入的 tree 执行:command:`git ls-tree`命令。

        如果想要递归显示目录内容，则使用 -r 参数调用。使用参数 -t 可以把递归过程遇到的每棵树都显示出来，而不只是显示最终的文件。

    不要使用 :command:`git commit -a`
        实际上Git的提交命令（:command:`git commit`）可以带上 -a 参数，对本地所有变更的文件执行提交操作，包括本地修改的文件，删除的文件，但不包括未被版本库跟踪的文件。
        这个命令的确可以简化一些操作，减少用:command:`git add`命令标识变更文件的步骤，但是如果习惯了使用这个“偷懒”的提交命令，就会丢掉Git暂存区带给用户最大的好处：对提交内容进行控制的能力。


Git对象
    見文件夾Git存儲對象圖片
        對象庫：
            對象庫存儲每次commit的所有信息,
                1、commit-信息
                    1、此commit的ID哈希值
                    2、此commit指向tree-ID的哈希
                    3、此commit父提交(上次提交)ID的哈希值
                    4、Author
                2、commit-tree
                    1、提交的目錄數
                        1、包含每個文件對應ID的哈希值
                3、commit-内容
                    1、該文件對應ID的哈希值
                        1、該文件具體内容
        暫存區：
            暫存區包含上次add的目錄，且提交内容會在的對象庫中生成。提交后add中目錄樹將會更新到object區域
                （objects标识的区域为Git的对象库，实际位于:file:`.git/objects`目录下，
                当对工作区修改（或新增）的文件执行:command:`git add`命令时，暂存区的目录树
                被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。
                当执行提交操作（:command:`git commit`）时，暂存区的目录树写到版本库（对象
                库）中，master分支会做相应的更新。即master最新指向的目录树就是提交时原暂存区的目录树。）
        引用命名空間：
        现在来看看HEAD和master的奥秘吧
            当前版本库中，HEAD、master和refs/heads/master具有相同的指向
            :file:`.git/HEAD`和:file:`.git/refs/heads/master`

            目录:file:`.git/refs`是保存引用的命名空间，其中:file:`.git/refs/heads`目录下的
            引用又称为分支。

    相關git指令：
    //查看上次提交原始信息
    git log -1 --pretty=raw
        commit e26b1a5ffd1ebde0a9311ae1ae5253a0b5967032
        tree a381f023e37424cee362c97be8105112cb6b11ea
        parent 2d8343b8fdc02ff21acf71d49a67e97c399b85d3
        author MeredithRowe <MeredithRowe@163.com> 1697101903 +0800
        committer MeredithRowe <MeredithRowe@163.com> 1697101903 +0800

            add Gemini_Mini_A_0001
    //查看哈希對應文件類型
    git cat-file -t e26b
    //查看哈希對應文件内容
    git cat-file -p e26b

    提交（Commit）对象之间相互关联，通过相互之间的关联则很容易的识别出一条跟踪链。
    这条跟踪链可以在运行:command:`git log`命令时，通过使用 --graph 参数看到。
    下面的命令还使用了 --pretty=raw 参数以便显示每个提交对象的parent属性
    git log --pretty=raw --graph e26b

    //顯示工作區狀態，显示工作区状态时，除了使用了 -s 参数以显示精简输出外，还使用了 -b 参数以便能够同时显示出当前工作分支的名称。
    git status -s -b
    ## master
    //分支管理的主要命令，也可以显示当前的工作分支。星号表明这个分支是当前工作分支
    git branch
    * master
    //顯示同一個分支
    git log -1 HEAD
    git log -1 master
    git log -1 refs/heads/master

问题：SHA1哈希值到底是什么，如何生成的？
    Linux下:command:`sha1sum`命令可以用于生成摘要
    //字符串 String 的SHA1哈希值为40个十六进制的数字组成
    $ echo -n String |sha1sum
    3df63b7acb0522da685dad5fe84b81fdd7b25264 *-

    //使用:command:`git cat-file`命令,查看文件内容
    $ git cat-file blob HEAD:welcome.txt
    Hello.
    Nice to meet you.

    //查看文件大小
    $ git cat-file blob HEAD:welcome.txt | wc -c
    25

    //在文件内容的前面加上 blob 25<null> 的内容，然后执行SHA1哈希算法
    $ ( printf "blob 25\000"; git cat-file blob HEAD:welcome.txt ) | sha1sum
    fd3c069c1de4f4bc9b15940f490aeb48852f3c42 -

    //上面命令得到的哈希值和用:command:`git rev-parse`看到的是一样的。
    $ git rev-parse HEAD:welcome.txt
    fd3c069c1de4f4bc9b15940f490aeb48852f3c42

    注意：
        1、采用部分的SHA1哈希值。不必写全40位的哈希值，只采用开头的部分，不和现有其他的冲突即可。
        2、使用 master 代表分支 master 中最新的提交，使用全称 refs/heads/master 亦可。
        3、使用 HEAD 代表版本库中最近的一次提交。
        4、符号` ^ 可以用于指代父提交。例如：
            HEAD^ 代表版本库中上一次提交，即最近一次提交的父提交。
            HEAD^^ 则代表 HEAD^ 的父提交。
        5、对于一个提交有多个父提交，可以在符号 ^ 后面用数字表示是第几个父提交。例如：
            a573106^2 含义是提交 a573106 的多个父提交中的第二个父提交。
            HEAD^1 相当于 HEAD^ 含义是HEAD多个父提交中的第一个。
            HEAD^^2 含义是 HEAD^ （HEAD父提交）的多个父提交中的第二个。
        6、符号 ~<n> 也可以用于指代祖先提交。下面两个表达式效果等同：
            a573106~5
            a573106^^^^^
        7、提交所对应的树对象，可以用类似如下的语法访问。
            a573106^{tree}
        8、某一此提交对应的文件对象，可以用如下的语法访问。
            a573106:path/to/file
        9、暂存区中的文件对象，可以用如下的语法访问。
            :path/to/file

    //查看當前分支的哈希值
    $ git rev-parse HEAD
    $ git cat-file -p e695
    $ git cat-file -p e695^
    $ git rev-parse e695^{tree}
    $ git rev-parse e695^^{tree}

Git重置
    //command:`git log`命令中使用了 --oneline 参数，类似于 --pretty=oneline ，但是可以显示更短小的提交ID
    $ git log --graph --oneline
        Cannot use lesskey file "//.less"
        * e26b1a5 (HEAD -> master) add Gemini_Mini_A_0001
        * 2d8343b say bye.
        * 8b3600c which version check in?
        * 3d64d7a initialized

    分支游标master的探秘
        引用 refs/heads/master 就好像是一个游标，在有新的提交发生的时候指向了新的提交。
        Git提供了:command:`git reset`命令，可以将“游标”指向任意一个存在的提交ID
        (命令中使用了 --hard 参数，会破坏工作区未提交的改动)
        $ git reset --hard HEAD^
        HEAD is now at e26b1a5 add Gemini_Mini_A_0001

    用reflog挽救错误的重置
        查看一下master分支的日志文件:file:`.git/logs/refs/heads/master`中的内容
        $ tail -5 .git/logs/refs/heads/master
        8b3600c31c18b663314eef984cf974193fcf4479 2d8343b8fdc02ff21acf71d49a67e97c399b85d3 MeredithRowe <MeredithRowe@163.com> 1697101544 +0800      commit: say bye.
        2d8343b8fdc02ff21acf71d49a67e97c399b85d3 e26b1a5ffd1ebde0a9311ae1ae5253a0b5967032 MeredithRowe <MeredithRowe@163.com> 1697101903 +0800      commit: add Gemini_Mini_A_0001
        e26b1a5ffd1ebde0a9311ae1ae5253a0b5967032 2da7d2e3c3fd62a7790604ca46f09006e03b2aa6 MeredithRowe <MeredithRowe@163.com> 1697177612 +0800      commit: does master follow this new commit?
        2da7d2e3c3fd62a7790604ca46f09006e03b2aa6 e26b1a5ffd1ebde0a9311ae1ae5253a0b5967032 MeredithRowe <MeredithRowe@163.com> 1697178024 +0800      reset: moving to HEAD^
        e26b1a5ffd1ebde0a9311ae1ae5253a0b5967032 2d8343b8fdc02ff21acf71d49a67e97c399b85d3 MeredithRowe <MeredithRowe@163.com> 1697178277 +0800      reset: moving to 2d834

        //通過下面命令實現查看文件内容
        $ git reflog show master | head -5
        2d8343b master@{0}: reset: moving to 2d834
        e26b1a5 master@{1}: reset: moving to HEAD^
        2da7d2e master@{2}: commit: does master follow this new commit?
        e26b1a5 master@{3}: commit: add Gemini_Mini_A_0001
        2d8343b master@{4}: commit: say bye.

        //重置master为两次改变之前的值
        $ git reset --hard master@{1}
        Updating files: 100% (432/432), done.
        HEAD is now at e26b1a5 add Gemini_Mini_A_0001

    深入了解 :command:`git reset` 命令
        用法一： git reset [-q] [<commit>] [--] <paths>...
            其中 <commit> 都是可选项，可以使用引用或者提交ID，如果省略<commit> 则相当于使用了HEAD的指向作为提交ID
            第一种用法在命令中包含路径:file:`<paths>`。为了避免路径和引用（或者提交ID）同名而冲突，可以在:file:`<paths>`前用两个连续的短线（减号）作为分隔。

            第一种用法（包含了路径:file:`<paths>`的用法） 不会重置引用，更不会改变工作区，而是用指定提交状态（<commit>）下的文件（<paths>）替换掉暂存区中的文件。
            例如命令:command:`git reset HEAD <paths>`相当于取消之前执行的:command:`git add <paths>`命令时改变的暂存区

        用法一： git reset [--soft | --mixed | --hard | --merge | --keep] [-q] [<commit>]
            第二种用法（不使用路径:file:`<paths>`的用法）则会 重置引用。根据不同的选项，可以对暂存区或者工作区进行重置

            使用參數：
                --hard
                1、替换引用的指向。引用指向新的提交ID。
                2、替换暂存区。替换后，暂存区的内容和引用指向的目录树一致。
                3、替换工作区。替换后，工作区的内容变得和暂存区一致，也和HEAD所指向的目录树内容相同
                --soft
                1、只更改引用的指向，不改变暂存区和工作区
                --mixed //默認缺省值
                更改引用的指向以及重置暂存区，但是不改变工作区

            示例
                git reset/git reset HEAD
                    用HEAD指向的目录树重置暂存区，工作区不会受到影响，相当于将之前用:command:`git add`命令更新到暂存区的内容撤出暂存区。
                    引用也未改变，因为引用重置到HEAD相当于没有重置

                git reset --filename
                    仅将文件:file:`filename`撤出暂存区，暂存区中其他文件不改变。相当于对命令:command:`git add filename`的反向操作

                git reset --soft HEAD^
                    工作区和暂存区不改变，但是引用向前回退一次。当对最新提交的提交说明或者提交的更改不满意时，撤销最新的提交以便重新提交。

恢复进度
    继续暂存区未完成的实践
        清除:file:`welcome.txt`的改动用检出命令
        $ git checkout -- welcome.txt

        删除本地多余的目录和文件，可以使用:command:`git clean`命令。先来测试运行以便看看哪些文件和目录会被删除，以免造成误删。
        $ git clean -nd
        Would remove a/

        真正开始强制删除多余的目录和文件
        $ git clean -fd
        Removing a/

   使用 :command:`git stash`
        命令：:command:`git stash`
        保存当前工作进度。会分别对暂存区和工作区的状态进行保存

        命令：:command:`git stash list`
        显示进度列表。此命令显然暗示了:command:`git stash`可以多次保存工作进度，并且在恢复的时候进行选择。

        命令：:command:`git stash pop [--index] [<stash>]`
        如果不使用任何参数，会恢复最新保存的工作进度，并将恢复的工作进度从存储的工作进度列表中清除。

        如果需要在保存工作进度的时候使用指定的说明，必须使用如下格式：
        git stash save "message..."

        命令：:command:`git stash apply [--index] [<stash>]`
        除了不删除恢复的进度之外，其余和:command:`git stash pop`命令一样

        命令：:command:`git stash drop [<stash>]`
        删除一个存储的进度。缺省删除最新的进度。

        命令：:command:`git stash clear`
        删除所有存储的进度。

    探秘 :command:`git stash`
        在执行:command:`git stash`命令时，Git实际调用了一个脚本文件实现相关的功能，这个脚本的文件名就是:file:`git-stash`。
        看看:file:`git-stash`安装在哪里了
        $ git --exec-path
注意：   /usr/lib/git-core

注意：  本地没有被版本控制系统跟踪的文件并不能保存进度。因此本地新文件需要执行添加git add再执行git stash

        git reflog show refs/stash
        git reflog show master | head -5

        //展示log中前兩條stash情況
        $ git log --graph --pretty=raw refs/stash -2

        //第幾次保存進度
        第一次进度保存可以用reflog中的语法，即用 refs/stash@{1} 来访问，也可以用简称 stash@{1}
        類似：$ git reset --hard master@{1}

        //展示第一個保存點的前三個提交信息
        git log --graph --pretty=raw stash@{1} -3
        理解：
            每個stash會保存當前狀態下的原基綫、原暫存區、原工作區，以及其他正常的版本的commit
            其中前三個依次是：原工作區、原暫存區、原基綫

        //原基线和原暂存区的差异比较
        $ git diff stash@{1}^2^ stash@{1}^2
        //原暂存区和原工作区的差异比较
        $ git diff stash@{1}^2 stash@{1}
        //原基线和原工作区的差异比较
        $ git diff stash@{1}^1 stash@{1}

        //从 stash@{1} 来恢复进度
        $ git stash apply stash@{1}

Git基本操作
    里程碑
    通过记录提交ID（或者创建Tag对象）来为当前版本库状态进行“留影”。
    $ git tag -m "Say bye-bye to all previous practice." old_practice

    留过影之后，可以执行:command:`git describe`命令显示当前版本库的最新提交的版本号。
    显示的时候会选取离该提交最近的里程碑作为“基础版本号”，后面附加标识距离“基础版本”的数字以及该提交的SHA1哈希值缩写。
    命令:command:`git describe`的输出可以作为软件版本号，这个功能非常有用。因为这样
    可以很容易的实现将发布的软件包版本和版本库中的代码对应在一起，当发现软件包包含
    Bug时，可以最快、最准确的对应到代码上。

    $ git describe
    new_practice

    看看版本库当前的状态，暂存区和工作区都包含修改
    $ git status -s

    通过下面的命令，可以看到在暂存区（版本库）中文件
    $ git ls-files

    本地刪除文件即rm *只會刪除本地文件不會影響暫存區内容，如果連同暫存區使用git rm *
    对于不想删除的文件执行:command:`git checkout -- <file>`可以让文件在工作区重现。
    儅執行 git rm *后暫存區内容被刪除，然後執行commit提交,最新版本庫中的内容也被刪除
    但是并不會影響歷史版本庫中的内容

    命令 :command:`git add -u` 快速标记删除
    执行:command:`git add -u`命令可以将（被版本库追踪的）本地文件的变更（修改、删除）全部记录到暂存区中。
    $ git add -u

    执行:command:`git add -A`命令会对工作区中所有改动以及新增文件(需要注意新增的文件也會添加到)添加到暂存区，也是一个常用的技巧。
    $ git add -A
    $ git status -s
    A welcome.txt

注意：   //add -u 與 -A的區別
        git add -u [<path>]: 把<path>中所有tracked文件中被修改过或已删除文件的信息添加到索引库。它不会处理untracted的文件。
        git add -A: [<path>]表示把<path>中所有tracked文件中被修改过或已删除文件和所有untracted的文件信息添加到索引库


    移动文件
        Git提供了:command:`git mv`命令完成改名操作。
        改名操作实际上相当于对旧文件执行删除，对新文件执行添加，即完全可以不使用:command:`git mv`操作，
        而是代之以:command:`git rm`和一个:command:`git add`操作。

    使用 :command:`git add -i`

    文件忽略
        Git提供了文件忽略功能。当对工作区某个目录或者某些文件设置了忽略后，再执行:command:`git status`查看状态时，
        被忽略的文件即使存在也不会显示为未跟踪状态，甚至根本感觉不到这些文件的存在。

        文件:file:`.gitignore`的作用范围是其所处的目录及其子目录，因此如果把刚刚创建
        的:file:`.gitignore`移动到上一层目录（仍位于工作区内）也应该有效。

        实际上面写的忽略文件不是非常好，为了忽略:file:`version.h`，结果使用了通配
        符 *.h 会把源码目录下的有用的头文件也给忽略掉，导致应该添加到版本库的文件忘记添
        加。

        忽略只对未跟踪文件有效，对于已加入版本库的文件无效

    本地独享式忽略文件
        ？

    文件归档
        如果使用压缩工具（tar、7zip、winzip、rar等）将工作区文件归档，一不小心会把版本
        库（:file:`.git`目录）包含其中，甚至将工作区中的忽略文件、临时文件也包含其中。
        Git提供了一个归档命令：:command:`git archive`，可以对任意提交对应的目录树建立归
        档。

        基于最新提交建立归档文件:file:`latest.zip`。
        $ git archive -o latest.zip HEAD

        只将目录:file:`src`和:file:`doc`建立到归档:file:`partial.tar`中
        $ git archive -o partial.tar HEAD src doc

        基于里程碑v1.0建立归档，并且为归档中文件添加目录前缀1.0
        $ git archive --format=tar --prefix=1.0/ v1.0 | gzip > foo-1.0.tar.gz

    Git克隆
        使用:command:`git clone`命令建立版本库克隆，
        以及如何使用:command:`git push`和:command:`git pull`命令实现克隆之间的同步

        Git使用:command:`git clone`命令实现版本库克隆，主要有如下三种用法：
            用法 1: git clone <repository> <directory>
            用法 2: git clone --bare <repository> <directory.git>
            用法 3: git clone --mirror <repository> <directory.git>

            用法1将 <repository> 指向的版本库创建一个克隆到:file:`<directory>`目录。目
            录:file:`<directory>`相当于克隆版本库的工作区，文件都会检出，版本库位于工作
            区下的:file:`.git`目录中。
            用法2和用法3创建的克隆版本库都不含工作区，直接就是版本库的内容，这样的版本
            库称为裸版本库。一般约定俗成裸版本库的目录名以:file:`.git`为后缀，所以上面
            示例中将克隆出来的裸版本库目录名写做:file:`<directory.git>`。

            用法3区别于用法2之处在于用法3克隆出来的裸版本对上游版本库进行了注册，这样可
            以在裸版本库中使用:command:`git fetch`命令和上游版本库进行持续同步

    Git的PUSH和PULL命令的用法相似，使用下面的语法：
        git push [<remote-repos> [<refspec>]]
        git pull [<remote-repos> [<refspec>]]

        其中方括号的含义是参数可以省略， <remote-repos> 是远程版本库的地址或名
        称， <refspec> 是引用表达式，暂时理解为引用即可。



    對等工作區：
        不使用 --bare 或者 --mirror 创建出来的克隆包含工作区，这样就会产生两个包含工作区的版本库。这两个版本库是对等的

        //克隆對等工作區到。/backup
        $ git clone ./ ./backup
        //原工作區進行提交
        $ git commit --allow-empty -m "sync test 1"
        $ git commit --allow-empty -m "sync test 2"
        //將commit push到克隆工作區
        $ git push ./backup
            注意：此時或報錯，如果强行這樣，如果您一意孤行，也不是不允许，但是您需要为我设置如下参数：
            receive.denyCurrentBranch = ignore|warn
        //進入備份工作區進行pull
        $ git pull
            为什么执行 git pull 拉回命令没有像执行 git push 命令那样提供那么多的参数呢？
            这是因为在执行:command:`git clone`操作后，克隆出来的demo-backup版本库中对源版本
            库（上游版本库）进行了注册，所以当在 demo-backup 版本库执行拉回操作，无须设置上游版本库的地址。

        //查看上游版本庫信息
        $ git remote -v
        origin  E:/书架/Git/./ (fetch)
        origin  E:/书架/Git/./ (push)

        //实际注册上游远程版本库的奥秘都在Git的配置文件中
        $ cat ./backup/.git/config

    克隆生成裸版本库
        在对等工作区模式下，工作区之间执行推送，可能会引发大段的错误输出，如果采用裸版本库则没有相应的问题。
        这是因为裸版本库没有工作区。没有工作区还有一个好处就是空间占用会更小

        //通過--bare進行克隆生成儸版本庫
        $ git clone --bare /path/to/my/workspace/demo /path/to/repos/demo.git

        //直接推送
        $ git push /path/to/repos/demo.git

    創建生成儸版本庫
        裸版本库不但可以通过克隆的方式创建，还可以通过:command:`git init`命令以初始化的方式创建
        但是git init是帶版本庫的，可以通過--bare進行創建儸版本庫
        $ git init --bare /path/to/repos/demo-init.git

        此時版本庫是空的需要push内容，但是如果執行push會出現問題
        $ git push /path/to/repos/demo-init.git
            原因：
            版本库刚刚初始化完成，还没有任何提交更不要说分支了。
            当执行:command:`git push`命令时，如果没有设定推送的分支，而且当前分支也没有注册到远程某个分支，
            将检查远程分支是否有和本地相同的分支名（如master），如果有，则推送，否则报错。
            所以需要把:command:`git push`命令写的再完整一些。像下面这样操作，就可以完成向空的裸版本库的推送。

            $ git push /path/to/repos/demo-init.git master:master


git分支
    新版本的开发往往是和当前版本同步进行的。如果两个版本的开发都混杂在master分支中，肯定会是一场灾难。
    从应用的角度上介绍分支的几种不同类型：发布分支、特性分支和卖主分支

    发布分支/BUG分支
        使用版本控制系统的分支功能，可以避免对已发布的软件版本进行bug修正时引入新功能的代码，或者因误删其他bug修正代码导致已修复问题重现。
        在这种情况下创建的分支有一个专有的名称：bugfix分支或发布分支（ReleaseBranch）。
    特性分支
        采用分支将某个功能或模块的开发与开发主线独立出来，是解决类似问题的办法，
        这种用途的分支被称为特性分支（Feature Branch）或主题分支（Topic Branch）。
    卖主分支
        所谓卖主分支，就是在版本库中创建一个专门和上游代码进行同步的分支，
        一旦有上游代码发布就检入到卖主分支中。图18-5就是一个典型的卖主分支工作流程

    分支命令概述
        用法 1 ： git branch
            用法1用于显示本地分支列表。当前分支在输出中会显示为特别的颜色，并用星号 “*” 标识出来。
        用法 2 ： git branch <branchname>
        用法 3 ： git branch <branchname> <start-point>
            用法2和用法3用于创建分支。
            用法2基于当前头指针（HEAD）指向的提交创建分支，新分支的分支名
            为 <branchname> 。
            用法3基于提交 <start-point> 创建新分支，新分支的分支名
            为 <branchname> 。
        用法 4 ： git branch -d <branchname>
        用法 5 ： git branch -D <branchname>
            用法4和用法5用于删除分支。
            用法4在删除分支 <branchname> 时会检查所要删除的分支是否已经合并到
            其他分支中，否则拒绝删除。
            用法5会强制删除分支 <branchname> ，即使该分支没有合并到任何一个分
            支中。
        用法 6 ： git branch -m <oldbranch> <newbranch>
        用法 7 ： git branch -M <oldbranch> <newbranch>
            用法6和用法7用于重命名分支。
            如果版本库中已经存在名为 <newbranch> 的分支，用法6拒绝执行重命
            名，而用法7会强制执行。

    Hello World开发计划

    創建新版本里程
    $ git tag -m "Release 1.0" v1.0



    基於特性開發的新分支
    开发者user1负责用getopt进行命令行解析的功能
            创建分支 user1/getop
            $ git branch user1/getopt

            使用:command:`git branch`创建分支，并不会自动切换。查看当前分支可以看到仍然工作在 master 分支（用星号 “*” 标识）中
            $ git branch
            * master
            user1/getopt

            执行:command:`git checkout`命令切换到新分支上。 (此時星號已經落在user1/getopt上)
            $ git checkout user1/getopt
            Switched to branch 'user1/getopt'

注意：      分支实际上是创建在目录:file:`.git/refs/heads`下的引用，版本库初始时创建的 master 分支就是在该目录下。

            在user1/getopt分支下創建文件並添加,設置tag,提交
            $ git add user1_branch.txt
            $ git commit -m "user1_branch.txt"
            $ git tag -m "user1 branch" user1_branch
            $ git describe

            切換到master分支並開始合并
            $ git checkout master
            $ git merge user1/getopt

            删除 user1/getopt 分支
            $ git branch -d user1/getopt

            reset合并後的内容到master工作區
            $ git reset --hard HEAD


        开发者user2负责多语种支持的功能
            使用chechout -b實現創建分支並切換到此分支
            git checkout -b <new_branch> [<start_point>]

    基于发布分支的开发
        要想解决在1.0版本中发现的bug，就需要基于1.0发行版的代码创建发布分支。
        創建發佈分支

        //查看當前tag版本
        $ git tag -n1 -l v*
        v1.0            Release 1.0

        //基於v1.0創建新分支
        $ git checkout -b hello-1.x v1.0
        Switched to a new branch 'hello-1.x'
        .....


    分支變基
        揀選命令：
            在git中，pick常与cherry配合使用，“cherry-pick”命令用于将指定的提交应用于其他分支，语法为“git cherry-pick commitHash”；该命令也支持一次转移多个提交到当前分支
            $ git cherry-pick jx/v1.0-i18n


            //切換到i18n分支並執行變基操作
            $ git checkout user2/i18n
            $ git rebase master





其他資料：
    https://www.php.cn/faq/506208.html
        5.设置SSH代理
        在使用Git时，我们可以通过SSH协议来访问远程仓库。为了提高访问速度，有时我们需要设置SSH代理来进行加速。











































