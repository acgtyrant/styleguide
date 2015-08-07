# styleguide

编程可谓艺术，风格（Style）则可因人而异，如空格者用空格制表符者用制表符，大写者用大写小写者用小写等。

但现代软件工程往往需要多人协同开发，风格的一致性至关重要。毕竟[人向来偏好他所熟悉的事物](http://www.douban.com/group/topic/39675260/)，于是若制定好统一的编程风格且得到团队成员普遍的认可，大家就不用再拘泥于各自的编程风格这种表面形式，把精力花在攻克旨要解决的真正问题上。

此外，好的编程风格不光保证一致性，还能教开发者学会避免常见的低级错误。比如在 C/C++ 中，你想把取地址符和解引用符放在哪边都可以，即 `int* a` vs `int *a`. 然而若贯彻后者，那开发者想把 `a` 和 `b` 都声明成 `int*` 时，就会头脑清醒地写成 `int *a, *b`, 反之，却有可能稀里糊涂地漏写成错误的 `int* a, b`.

所以你可以先观摩观摩**你所向往的组织**，学习他们所遵循的编程风格，更可以向开源项目贡献大家喜闻乐见的代码。Linux 有 [Linux kernel coding style](https://www.kernel.org/doc/Documentation/CodingStyle), GNU 也有 [GNU Coding Standards](http://www.gnu.org/prep/standards/standards.html), Google 更是一举推出了五花八门的 [Google Style Guides](https://github.com/google/styleguide).

## 暴君御用编程风格

我习惯一边学编程语言，一边掌握并贯彻公认的出色编程风格，这样可以少走很多弯路。特此列出御用编程风格并谈谈心得，一般而言，我所有个人的项目均贯彻御用编程风格。

### C++

Google C++ Style Guide 自然首当其冲地成为**御用 C++ 编程风格**。其实很早就有[前辈翻译成中文](http://zh-google-styleguide.readthedocs.org/en/latest/google-cpp-styleguide/contents/)，只不过年代已久远，连 C++11 都没涉及。于是我便花了点时间[更新翻译](http://zh-google-styleguide.readthedocs.org/en/latest/google-cpp-styleguide/contents/)，还加了新译者笔记，欢迎阅读。

此外将来我还要读一读 (More )Efficient C++, 读书笔记大概会更新到 cpp.md.

### C

《Ｃ陷阱与缺陷》该讲的都讲得差不多了，不过我最近在读《UNIX 环境高级编程》，略有编程风格上的新心得，会更新在 c.md 里，此外将来若我有志向 Linux, GNU 等项目贡献了，到时也许会总结出御用编程风格说不定。

### Python

令人费解的是，明明已经有了足够众所瞻望的编程风格 [PEP 0008](https://www.python.org/dev/peps/pep-0008/), Google 还[另立门户](https://google-styleguide.googlecode.com/svn/trunk/pyguide.html)。不过我现在还没有系统地学习 Python, 这艰难的抉择以后再说吧。

## 许可证

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">styleguide</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="github.com/acgtyrant/styleguide" property="cc:attributionName" rel="cc:attributionURL">acgtyrant</a> 创作，采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="acgtyrant.com" rel="cc:morePermissions">acgtyrant.com</a> 处获得。
