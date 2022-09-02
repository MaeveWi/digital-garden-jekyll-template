[gitlabRunner帮助文档](https://docs.gitlab.com/runner/)

Runners are the agents that run the CI/CD jobs that come from GitLab.

如何安装Runner：
You can view installation instructions in GitLab by going to your project’s **Settings > CI / CD**, expanding the **Runners** section, and clicking **Show runner installation instructions**. After you install GitLab Runner, you must [register individual runners](https://docs.gitlab.com/runner/register/index.html) with your GitLab instance. 

虽然可以安装在docker上，但是我们直接安装在机器上，用linux方式，注册时执行器填shell：
Enter an executor: virtualbox, docker+machine, docker-ssh+machine, kubernetes, docker, shell, parallels, ssh, custom, docker-ssh:  
**shell**

![[Pasted image 20220902175824.png]]

注册完成之后，就可以在gitlab-settings-CI/CD-Runners上看到可用的runners了，点击可以进行编辑

![[Pasted image 20220902180922.png]]