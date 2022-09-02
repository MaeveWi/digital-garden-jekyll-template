
### 管道（pipeline）

每个推送到 Gitlab 的提交都会产生一个与该提交关联的管道(pipeline)，若一次推送包含了多个提交，则管道与最后那个提交相关联，管道(pipeline)就是一个分成不同阶段(stage)的作业(job)的集合。


### .gitlab-ci.yml包含了你的项目如何被编译的描述语句：

#### Job

Job是.gitlab-ci.yml文件中最基本的元素，由一系列参数定义了任务启动时所要做的事情，用户可以创建任意个任务；每个任务必须有一个独一无二的名字，但有一些保留keywords不能用于Job名称，image，services，stages，types，before_script，after_script，variables，cache。

Job被定义为顶级元素，并且至少包括一条script语句，如果一个 Job 没有显式地关联某个 Stage，则会被默认关联到 test Stage。

#### stages

用于定义所有作业(job)可以使用的全局阶段，gitlab-ci.yml允许灵活定义多个阶段，stages元素的顺序定义了作业执行的顺序。Job关联的stage名相同时，该多个Job将并行执行（在拥有足够Runner情况下）。下一个阶段的job将会在前一个阶段的job都完成的情况下执行。

如果文件中没有定义 stages，那么则默认包含 build、test 和 deploy 三个 stage。Stage 中并不能直接配置任何具体的执行逻辑，具体的执行逻辑应该在 Job 中配置。

注：如果想要控制某一个stage在最开始，或者最后执行，可以使用.pre 和 .post 关键字

##### script

script是一段由Runner执行的shell脚本。

有些时候，script命令需要被单引号或者双引号所包裹。举个例子，命令中包涵冒号的时候，该命令需要被引号所包裹，这样YAML解析器才知道该命令语句不是“key: value”语法的一部分。当命令中包涵以下字符时需要注意打引号:: { } [ ] , & * #? | - < > = ! % @ `

##### only and except

-   only和except两个参数说明了job什么时候将会被创建：
-   only定义了job需要执行的所在分支或者标签
-   except定义了job不会执行的所在分支或者标签

以下是这两个参数的几条用法规则：

-   only和except如果都存在在一个job声明中，则所需引用将会被only和except所定义的分支过滤
-   only和except允许使用正则
-   only和except允许使用指定仓库地址，但是不forks仓库


链接：https://juejin.cn/post/7018141028632772621  



