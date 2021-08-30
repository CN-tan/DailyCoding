---
description: Notes of nginx
---

# Nginx



[来源: nginx文档](https://www.nginx.cn/doc/standard/httpcore.html)

**使用方式: location \[=\|~\|~\*\|^~\] /uri/ { ... }** 默认值:无 使用场景: server内,即

```bash
server{
    ...
    location ... {
    }
}
```

这项指令可以根据URI来执行不同的路由方式,你可以使用普通字符串或是正则来配置location指令.使用正则表达式时需要加一个前缀

```bash
location ~*   #大小写不敏感
location ~    #大小写敏感
```

在决定一个具体的query的去向\(跟哪条location指令相匹配\)时,nginx首先会检查字符串匹配,找到前缀匹配最多的那个.

> 例子: 现在有一个query: /image/delete location如下 `location = /image location = /image/delete`

然后开始按顺序检查正则表达式. 若能匹配,则query会跑到第一个能用正则匹配的location下; 若不能匹配,则使用上一步字符串匹配的结果.

你可能会问: 想匹配的查询既能字符串匹配,也能正则匹配,而我就想用字符串的结果,该怎么办? 有两种方法:

1. **使用前缀 "="** 

   带有这个的location只会匹配完全相同的字符串,并且在匹配到后停止后续的正则匹配. 举例来说,我们经常用到的"/" 就可以用"location = /"来完全匹配

2. **使用前缀"^~"**

   带有这个的location



