---
title: idea 配置缓存历史记录
date: 2018-07-10 21:09:19
tags: 开发工具
---
#### [All the files are located under this directory by default:](https://intellij-support.jetbrains.com/hc/en-us/articles/206544519-Directories-used-by-the-IDE-to-store-settings-caches-plugins-and-logs)

Windows Vista, 7, 8, 10:

<SYSTEM DRIVE>\Users\<USER ACCOUNT NAME>\.<PRODUCT><VERSION>

Under this directory you'll find the following sub-directories

config: configuration (idea.config.path)

config\plugins: plugins (idea.plugins.path)

system: caches, local history, etc (idea.system.path)

system\log: logs and thread dumps (idea.log.path)

#### [change the defaults](https://intellij-support.jetbrains.com/hc/en-us/articles/207240985-Changing-IDE-default-directories-used-for-config-plugins-and-caches-storage?sort_by=created_at)
Follow the comments in IDE_HOME\bin\idea.properties file to change the defaults, make sure to uncomment the lines defining these properties:
idea.config.path
idea.system.path
idea.plugins.path
idea.log.path
Example:
```
idea.config.path=c:/work/idea/caches/trunk-config
idea.system.path=c:/work/idea/caches/trunk-system
idea.plugins.path=c:/work/idea/caches/trunk-plugins
```

#### [IDE Settings](https://www.jetbrains.com/help/idea/project-and-ide-settings.html)
IDE settings are stored in the dedicated directories under IntelliJ IDEA home directory. The IntelliJ IDEA directory name is composed of the product name and version.

For IntelliJ IDEA Community edition the folder name is .IdeaICXX.

For example:

Windows
```
<User home>\.IntelliJIdeaXX\config that contains user-specific settings.
<User home>\.IntelliJIdeaXX\system that stores IntelliJ IDEA data caches.
<User home> in WindowsXP is C:\Documents and Settings\<User name>\;
```
in Windows Vista it is C:\Users\<User name>\
