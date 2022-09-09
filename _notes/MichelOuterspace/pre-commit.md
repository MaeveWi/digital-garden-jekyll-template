---
title: pre-commit
---
## What
[[Git hooks]]中的一个钩子。

也是一个同名工具项目，用于管理和维护多语言Hooks的框架。pre-commit框架，随着发展，已经不单单只能用于git hooks的pre-commit阶段，而是能作用于所有git hooks的所有阶段。

==[官方文档](https://pre-commit.com/)==

## How
1.  安装
    
    ```
    # 直接使用pip安装
    pip install pre-commit
    ```
    
    安装成功后，使用`pre-commit --version`可正常查看版本。
    
2.  创建配置文件  
	**需要手动在项目根目录创建`.pre-commit-config.yaml`配置文件。**
    
    ```
    # 在根目录执行如下命令，使用官方示例生成一个默认的配置，python版本
    pre-commit sample-config > .pre-commit-config.yaml
    ```
    
3.  创建git hooks钩子脚本  
    pre-commit框架还需要通过git hooks本身的钩子来调用。
    
    所以在设置好配置文件后，需要根据配置，在git项目中将钩子脚本添加到`.git/hooks`路径下。
    
    使用以下命令，可以自动配置对应的`hooks`脚本到`.git/hooks`中
    
    ```
    # 直接执行此命令，设置git hooks钩子脚本
    pre-commit install
    ```
    
4.  对所有文件进行一次检查 (可选)  
    配置设置好后，默认是需要`git commit`命令来出发调用的，只会检查`git commit`中变更的文件。对所有文件进行检查：
    
    ```
    # 直接执行此命令，进行全文件检查
    pre-commit run --all-files
    ```

## .pre-commit-config.yaml配置详细说明

```yml
# 设置默认的阶段为push，只在提交时进行检查
default_stages: [push]
repos:
  #git clone的存储库url
  - repo: https://github.com/pre-commit/pre-commit-hooks
    #git clone要拉取的tag或者revision
    rev: v2.4.0
    #这个库中具体的哪些hooks脚本：
    hooks:
        #hooks下层又有多个配置：id,name,args,stages等，具体看官方文档
      - id: check-yaml  #Attempts to load all yaml files to verify syntax.
      - id: end-of-file-fixer #Makes sure files end in a newline and only a newline.
      - id: trailing-whitespace #Trims trailing whitespace
        args: [--markdown-linebreak-ext=md] #To preserve Markdown hard linebreaks
  - repo: https://github.com/pre-commit/mirrors-yapf
    rev: v0.29.0
    hooks:
      - id: yapf 
        args:
          [
            --style,
            "{based_on_style: google, indent_width: 4, COLUMN_LIMIT: 120}",
          ]
```

首先，是顶层的全局配置，配置项有如下这些：

- **repos：**（必需）最重要的核心配置，用来告诉pre-commit从哪里获取钩子的代码。pre-commit官方支持的所有Hooks：==[Hooks](https://pre-commit.com/hooks.html)==
- **default_stages：**（可选）默认值：all stages，设置覆盖的默认stages。只覆盖没有设置stages的单个钩子。
- default_language_version：（可选）从语言到应该用于该语言的默认language_version的映射。这将只覆盖没有设置language_version的单个钩子。默认为：{}
   ```yaml
   # 设置默认的语言版本，你也可以在每个repos中单独设置language_version
	default_language_version:
	  python: python3.7 
   ```
- files：（可选）全局文件包含，正则匹配模版，1.21.0新配置，默认值：""
- exclude：（可选）全局文件排除，正则匹配模版，1.1.0版本新配置，默认值：^$
- fail_fast：（可选）设置为true时，预提交将在第一次失败后停止运行钩子。1.1.0版本新配置
- minimum_pre_commit_version：（可选）需要pre-commit的最小版本。1.15.0版本新配置

## 本地自动启用pre-commit

看上面的介绍和使用，会发现有个问题。我从git库中clone一个项目到本地后，即使项目中有`.pre-commit-config.yaml`配置文件，但是`.git/hooks`中还是没有设置钩子，需要运行`pre-commit install`安装后，才能正常使用。

如何让他根据`.per-commit-config.yaml`配置自动安装git钩子呢。让我们直接clone项目后，便自动启用了pre-commit。

官方给了一个解决方式：  
使用pre-commit init-templatedir命令，自动设置git项目的初始化模版，在版本中自动执行`pre-commit install`以启用pre-commit。

设置步骤如下：

```bash
# 设置git全局变量，制定初始化模版目录
git config --global init.templateDir ~/.git-template

# 自动设置初始化模版
pre-commit init-templatedir ~/.git-template
```

ok，到此就可以了，然后可以测试一下，clone一个带`.per-commit-config.yaml`配置的库，然后进行提交，则会自动进行pre-commit的检测。如果没有`.per-commit-config.yaml`配置，则会跳过，普通正常使用。