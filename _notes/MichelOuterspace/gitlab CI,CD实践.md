## 如何使用gitlab pipeline构建自动化: gitlab-ci

GitLab [[CI、CD|CI]]是GitLab内置的进行持续集成的工具，只需要在仓库根目录下创建.gitlab-ci.yml 文件，并配置[[GitLab Runner]]；每次提交的时候，gitlab将自动识别到.[[gitlab-ci.yml]]文件，并且使用Gitlab Runner执行该脚本。

创建gitlab-ci文件，可以直接点击add CI/CD ...，会自动创建一个模板文件，可以修改后提交
![[Pasted image 20220902183203.png]]

![[20220902175021.png]]

### 验证.gitlab-ci.yml

GitLab CI的每个实例都有一个名为Lint的嵌入式调试工具，它可以验证.gitlab-ci.yml文件的内容，进入项目仓库->CI/CD->CI Lint。

![[Pasted image 20220902183111.png]]