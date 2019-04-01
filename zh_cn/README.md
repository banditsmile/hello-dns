                <meta charset="utf-8" emacsmode="-*- markdown -*-">
                            **A warm welcome to DNS**

# 你好，欢迎了解DNS!

本系列文件试图对截至2018年的域名系统进行正确的介绍。原始的RFC仍然是规范性文本
的权威来源，但是本文档试图使这个古老的协议更容易访问，同时保持与所有相关和有用的RFC
的完全一致。

这项工作是在Github上合作开发的, 仓库地址在 [https://github.com/ahupowerdns/hello-dns/](这里) 
非常期待您的帮助!  反馈信息可以发给 bert.hubert@powerdns.com or
[@PowerDNS_Bert](https://twitter.com/PowerDNS_Bert).

目前贡献者包含: Michał Kępień, Jan-Piet Mens, Andrew Babichev,
Jacob Hoffman-Andrews, Peter van Dijk, Nathan Froyd, Gene McCulley,
Charles-Henri Bruyand, jose nazario, Warren Kumari, Patrick Cloke, 和
Andrew Tunnell-Jones.  感谢!

虽然我们从相对基本的原则出发，但读者是有希望的要知道什么是IP地址，什么是（根）
解析器，什么是权威服务器应该这样做。有疑问时：权威服务器“主机”DNS数据，
“解析器”在权威服务器上查找内容服务器和客户机运行“存根解析程序”来查看分解器。
本文档面向开发人员，但也可能有助于管理员。

DNS最初于1979年8月在'[IEN116]（https://www.rfc-editor.org/ien/ien116.txt）'，
并行的一部分描述互联网的一系列文件。 IEN 116时代的DNS不是与今天的DNS兼容。 
1983年，RFC 882和883发布，描述DNS的版本非常相似但不能完全互操作与我们今天拥有的一个。

当RFC 1034和1035发布时，DNS在1987年获得了现代形式。虽然1034/1035的大部分
仍然有效，但这些标准并不那么容易阅读因为它们是在非常不同的时间写的。 有100多个
只能在以后的文档中找到的更新页面。

这项工作的主要目标不是与DNS RFC相矛盾，而是为理解域名系统提供一个更容易的入口点。

如果你愿意，我们的目标是成为一个迷你“[TCP / IP图解说明]
（https://en.wikipedia.org/wiki/TCP/IP_Illustrated）“的DNS。更多关于这些
文件的哲学，以及如何贡献，请阅读[meta.md]（meta.md.html）。
非常欢迎您的帮助和见解！

我要感谢ÓlafurGuðmundsson和Job Snijders的改善DNS状态的热情意见和建议。

## 目录
下面的内容在接下来的每篇文章都会出现:

 * [DNS的核心](basic.md.html)
 * [与存根解析器和应用程序相关](stub.md.html)
 * [认证服务器相关](auth.md.html)
 * [解析器相关](resolver.md.html)
 * [tdns: 一个 '从零开始' 的DNS 库](tdns/README.md.html)
   * [tauth: 一个很小但是功能完善的认证服务器](tdns/tauth.md.html)
   * [tres: 一个很小但是功能完善的DNS解析器](tdns/tres.md.html)
   * [C API: a C library for doing DNS queries](tdns/c-api.md.html)
 * 可选组件: [EDNS, TSIG, Dynamic Updates, DNAME, DNS Cookies](optional.md.html)
 * [隐私相关](privacy.md.html): QName minimization, DNS-over-TLS, DNS-over-HTTPS, EDNS Padding
 * [DNSSEC](dnssec.md.html)
 * [非-IETF 规范](non-ietf.md.html): RRL and RPZ
 * [DNS稀有部分](rare.md.html) - 不会过时，但在生产中不会经常遇到

我们首先介绍DNS基础知识：什么是资源记录，什么是RRSET，什么是区域，什么是区域切割，
数据包是如何布局的。 对于任何想要查询名称服务器或发出有效响应的人来说，这部分都是必读的。

然后，我们专门研究应用程序在向解析器发送问题时可以预期的内容，或者存根解析器可以预期的内容。
下一部分是关于权威服务器应该做什么。 在此基础上，我们稍微详细描述一下旋转变压器的运行方式。 
最后，有一个关于可选元素的部分，如EDNS，TSIG，动态更新和DNSSEC。

RFC，尤其是早期的RFC，倾向于把认证功能和解析功能放在一起进行描述。结果导致更难编码和故障排除。
因此，在这些文档中，认证和缓存功能分开描述。

下一章: [DNS 基础](basic.md.html).

<!-- Markdeep: --><style class="fallback">body{visibility:hidden;white-space:pre;font-family:monospace}</style><script src="ext/markdeep.min.js"></script><script>window.alreadyProcessedMarkdeep||(document.body.style.visibility="visible")</script>
