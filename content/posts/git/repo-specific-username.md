---
title: "Git - Set repository specific config"
date: 2022-02-09T14:32:51+05:30
draft: false
---

Generally, for git, its good idea to set up repository specify username and email. Here is how you can do it.

```shell
 git config user.email "<your email id>"
 git config user.name "<Your Name>"
```

Use the following in case you want to to set up global username and name.

```shell
 git config --global user.email "<your email id>"
 git config --global user.name "<Your Name>"
```

Remember that local git config will always override the global git config. 


