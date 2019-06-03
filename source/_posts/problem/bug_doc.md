title: 测试文档编写
date: 2019-06-03 13:16:43
updated: 2019-06-03 13:16:43
tags:
  - document
categories:
  - problem
---

**Bug 描述**
A clear and concise description of what the bug is.

**复现**
复现步骤:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**预期结果**
A clear and concise description of what you expected to happen.

**截图**
If applicable, add screenshots to help explain your problem.


**附加信息**
Add any other context about the problem here.

## 单机服务卸流
- 漏桶算法

将流量放入桶中，漏桶同时也按照一定的速率流出，如果流量过快的话就会溢出(漏桶并不会提高流出速率)。溢出的流量则直接丢弃。

- 令牌桶算法

会以一个恒定的速率向固定容量大小桶中放入令牌，当有流量来时则取走一个或多个令牌。当桶中没有令牌则将当前请求丢弃或阻塞。

----

<details>
  <summary>Click to expand</summary>
  whatever
</details>

<details>
  <summary>Summary</summary>
  <code>
  js
  const x = 1
  
  </code>
</details>