title: 如何编写README文件
---
github是世界上最大的代码托管网站，相信不少人都在上面托管了自己的开源项目。对于开源项目来说，一个好的README文件是不可或缺的，这有助于其他人快速了解你的项目，使用你的项目并有可能对你的项目做出贡献。但很多人会觉得无从下笔，不知道应该写些什么，那么README文件到底应该写些什么呢？
<!--more-->
### 在书写之前
在github中，README文件一般使用markdown语言编写，markdown是一种简单的标记语言，语法简单，很快就能学会，非常适合用于编写文档，如果你还不熟悉markdown的语法，可以[在这里](https://www.appinn.com/markdown/)查看。

github的官网上对如何写README文档也有介绍，但内容比较少，我参考了许多文档，大概总结了一些内容。

下面列出在你的README文件中可以包含的信息。

**注意**：这里只是列出在README文件中可以包含的常见信息，并不是说下面的内容都必须包含，你应该根据你项目的具体情况来选择。

***
#### Project Title 项目名称
这个当然是毋庸置疑的啦，对于一个项目首先就应该写出它的名称。在名称下面还可以加上一段（不要太长）精简的对项目的描述。

#### introduction 介绍
在这里写上对项目的介绍。

#### Status 状态
在这里写上你项目所属的状态，例如当前项目处于哪个版本，项目大小，是否需要编译，下载次数等等信息。

在这里推荐大家使用状态徽章。
##### shields
这个徽章就是大家经常在github项目中看到的徽章，它们长这个样子：


[![Travis](https://img.shields.io/travis/rust-lang/rust.svg)]()  [![Coveralls github](https://img.shields.io/coveralls/github/jekyll/jekyll.svg)]()  [![Github Releases](https://img.shields.io/github/downloads/atom/atom/latest/total.svg)]()  [![npm](https://img.shields.io/npm/v/npm.svg)]()


是不是看起来很炫酷啊，这些徽章你可以在[shields](https://shields.io/)中获取，它们提供非常详尽的徽章内容，基本可以满足所有的状态介绍。

##### forthebadge
同样也是一个提供徽章的网站，这个网站的徽章更简约和扁平化。

[![forthebadge](http://forthebadge.com/images/badges/fuck-it-ship-it.svg)](http://forthebadge.com)

[![forthebadge](http://forthebadge.com/images/badges/powered-by-electricity.svg)](http://forthebadge.com)

你可以在[forthebadge](https://forthebadge.com/)的网站获取这些徽章。

这两种徽章完全凭你的喜好选择。

#### Features 特性
写出你的项目的功能特性，可以用来做什么。（最重要的是写出你的项目的优势在哪里）

#### Table of contents 内容目录
如果你的文档很长，可以添加一个目录，为读者做一个快速导航，方便读者快速找到自己想看的内容。

#### Documentation 文档
如果你的文档独立存在（拥有独立的文档网站），可以在这里写上你的文档地址。

#### Compiling 编译信息
如果你的项目需要编译，可以在这里写上项目的编译信息。

#### Downloads 下载
如果提供各种形势的项目下载方式，可以在这里列出来。

#### Installation 如何安装
在这里写出你的项目的安装方式。

#### Prerequisites 依赖
写出运行或使用你的项目的依赖项目及所需环境。

#### Quick start 快速开始
在这里写出一份简单的你的项目改如何使用的介绍，它应该包含你的项目从下载后到运行出一个最简单的示例的所有步骤。（也就是如何运行出一个hello world示例）

#### Test 测试
在这里解释如何运行这个系统的自动化测试。

#### Deployment 部署
在这里写有关如何在实时系统上进行部署的其他说明。

#### API Reference API参考
这是文档最重要的内容，对你的项目API做出详尽的介绍。

根据项目的规模，如果它足够小又简单，可以将参考文档添加到自述文件中。对于中型到大型项目，至少要提供API参考文档所在的链接。

#### Contributing 贡献
开源项目最大的优势就是群策群力，所有人都可以对项目做出贡献。在这里写上为你的项目做出贡献的方法。

#### Contributor 贡献者

在这里列出目前项目的贡献人或贡献团队和机构。

#### Issues 问题
一个项目不免会有些bug，在这里写出用户如何向你报告bug或是提问的方法。

#### Changelog 更新日志
你可以在这里写出项目版本更新的日志。

#### Authors 作者
在这里写出作者信息。

#### Communication 联系方式
写出如何联系到项目负责人的方式，可以是网站，电子媒体，电话，邮箱或通讯地址。

#### Community 社区
如果你的项目拥有周边社区或周边项目，可以在这里列出它们的介绍和链接。

#### License 协议
在这里写你的项目遵照的开源协议。如果你还不了解开源协议，可以看看这篇[文章](https://www.cnblogs.com/Wayou/p/how_to_choose_a_license.html)，可以帮你快速的了解和选择开源协议。

#### Acknowledgments 致谢
如果你有想感谢的对这个项目做出过贡献的人或是机构，可以写在这里。

以上就是我总结你可以在文档中写出来的常见内容，当然肯定会遗漏一些内容。再说一次，你的文档并不用拘泥于以上的形式，我这里只是列出一些参考，**重要的是**根据你项目的具体情况写出适合它的文档，对于不同的语言，不同的项目类型，肯定还有很多符合项目类型的具体的点要写出来，具体你还可以去参考github上与你的项目相近的项目的文档。

好啦。写文档去吧。
