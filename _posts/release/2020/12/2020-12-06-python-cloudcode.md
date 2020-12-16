---
layout: post
category: python
title: 都无代码编程了，编程还香吗
tagline: by 太阳雪
tags:
  - 云开发
  - 编程
---
11月29日（2020年），腾讯举行了一场主题为 “重新定义开发” 的[小程序开发技术峰会](https://mp.weixin.qq.com/s/xb-7dGo7SXbm4hVaE7QO5A)，发布的了新一代的云开发平台，用少量代码，甚至不用代码，就可以快速创建一个云应用，大幅降低应用开发门槛，让人人都能做开发，那么对于程序员以及打算学习编程的人来说，何去何从呢？
<!--more--->
## 云开发厉害在哪里

### 零运维

相比于传统的系统开发，云开发省去了服务器搭建、系统部署、域名申请、服务器运维等工作

同时提供了弹性的计算能力：当请求量达到一定值，服务器会自动扩容，提高性能，如果请求量减少到一定量，服务器会自动缩容，甚至降低到零，以节省计算资源的使用成本

如果传统开发模式，要到的这样的效果，需要一个技术力量强大的团队才能行，而所作的这些工作，与业务本身关系不大

### 简单易用

#### 鉴权

之前做个公众号或者小程序开发的童鞋，一定对微信复杂而繁琐的鉴权方式印象深刻，获取 accessToken 不但麻烦，而且还得在过期之前重新获取

使用云开发，会极大地简化了这个过程，并且弱化了相关概念，节省了工作量，降低了学习成本

在云开发平台上，原来各种复杂的事情，利用 `微信 SDK`（封装了各种接口的开发工具集），像调用普通本地方法一样简单

#### 数据库

数据库是应用重要的组成部分，不过在开发中，搭建数据库、设计库表、调试、运维，需要投入大量的精力和时间

云开发平台，提供了高可用的 NOSql 数据库，不仅无需搭建，还会自动扩容，将复杂的权限管理，简化为适应不同场景的简单配置

数据以 JSON 格式存储，便于理解，而且省去了数据格式来回转换的麻烦

配合数据库实例组件，可以实现业务上的各种操作方式

#### 文件存储

一般来说上传文件、照片等，需要文件存储的支持，传统做法是在服务器上指定存储位置，设置读写权限，如需要加速访问，还需要另购和调试 CDN 服务，极富挑战性

在云开发平台上，使用上传组件，可以轻松地将文件上传至云存储，并且自动支持 CDN 加速

和数据库权限类似，也将访问权限简化为适应不同应用场景的简单配置

### 免费

对个人开发者来说，应用上面提到的各种特性的云服务资源，是免费的！

![免费资源配置](http://justdopython.com/assets/images/2020/12/cloudcode/02.jpg)

5G 存储空间，5G CDN 月流量、2G 数据库容量、以及 1G 的出网流量，对普通的小程序应用来说，足够了

如果开发的小程序应用得到了市场认可，用户量上来了，可以方便地切换到按量付费模式，实现更强大的弹性计算能力，以支撑业务的增长

## 腾讯的野心

腾讯为什么要提供这么强大的平台和机会呢？难不成是在做慈善？

### 链接每个人

微信从 2011 年 1 月 21 日正式发布以来，到现在月活用户已超 12 亿，几乎链接了 “所有人”，已然形成了微信互联网

> 微信不再只是一个熟人间免费发消息的应用了。甚至，连互联网圈、投资圈里的人经常用来描述微信的那个词 —— 操作系统 —— 也彻底不够用了
> 微信干脆是个完整的互联网 —— 所有人都在上面的移动互联网 —— 也就是说，先是互联网吞噬了整个世界，而后，微信吞噬了互联网……
>
> ——《微信互联网平民创业》李笑来

### 链接每个系统

如果说微信完成了将人链接起来的使命，那么小程序云开发，就是要将所有应用链接起来，哪怕这个应用只是在你的想象当中

- 微信构筑了一个巨大的用户网，解决了传统系统构建中的注册、管理、单点登录等问题

- 云平台提供各种接口，同时提供多种数据导出备份机制，可以轻松的和其他系统关联

- 统一规格的 UI 组件，应有尽有，满足各种场景的展现和交互

- 降低开发门槛，提供免费开发资源

这些特性，是为了让更多的人参与到应用开发中来，特别是对那些有想法而没有能力付诸实践的人，利用云开发平台，即可轻松实现

## 何去何从

微信云开发的出现，只是一个开始，未来程序开发会变得更简单，功能更强大

原本用来安身立命的技术本领用不上了；

学习的个各种新技能知识过时了；

想作为资深程序员宣扬下编码技巧，开发无代码化了……

什么才是重要的？又该如何应对呢？

### 基础知识更重要

微信云开发，虽然简化了开发过程，让后台（指服务器端）变得不太重要，但所有的技术都是以互联网为基础，依赖于最基本的 Http 协议和基本的编程规范

也就是说，云开发会尽可能多地替代了纯技术，以及可以被自动化的部分，并且这个趋势会不大增大增快，会有更多的云厂商提供更好的自动化技术

而需要程序员做使用基础的编程技能做更多实现更多的业务逻辑

也就是，集中精力学习基础的编程逻辑，了解基本的计算机、网络知识更重要

例如，前端框架工具层出不穷，但都基于基本的 Html、CSS、和 JS 构建

例如，前端模块打包工具 Webpack，很好用，但学习成本高，很快被更为简单易用的 Taro 框架融合，屏蔽了 Webpack 在使用层面的复杂性

### 强化探索性学习

互联网的快速发展，促生了无数的技术，涉及到互联网技术的方方面面

面对爆炸式的技术增长，不可能面面俱到，学习所有的知识，哪怕是一个方向，不断地迭代也会使我们应接不暇

不禁有人喊出 “老子学不动了” 的呐喊：

![老子学不动了](http://justdopython.com/assets/images/2020/12/cloudcode/01.png)

那么应该如何去学呢？大概有几点建议

- 加强基础知识的学习
- 广泛地了解技术动态，了解当前的热门和当下正在解决的问题
- 将新的技术与基础知识相关联，或者用基础知识对技术进行分类
- 探索性的学习，不用从头到尾看，而是带着问题去了解，比如新框架的鉴权如何实现等

### 业务和想法更重要

机械化的编程，会越来越多地被机器替代，细节的基础架构，会快速地被简单易用的工具、框架完成

而具体的业务以及我们的想象力，不会被替代

既然有更多的技术支持，更低的开发门槛，我们就更容易地实现原本不容易，甚至不可能实现的的想法

现在不用担心实现问题，不用为搭建平台消耗精力，就会有更多的时间用于思考业务，和解决真正的问题

而业务知识和想象力是机器不具备的，也是无法被代替的，面对技术的发展，如何设计一个产品，去解决一个实际问题，变得更加重要了

想象以下，如果没有计算机技术的发展，我们每个人都离用计算机解决问题很远，那些只能是前沿科学家们才能做的事情

而如今，三两天就可以做出一个使用量超过 600 万的 `群登记助手` 小程序

## 总结

腾讯云开发其实不是程序员的克星，更像是一个称职的管家，是一个贴身的保镖，为我们节省了大量的非业务相关时间，为我们加强了系统平台的稳定性，提高了系统的计算性能，让我们可以全心全意学习核心知识、研究业务实质、构建优秀产品

因此，祝愿如虎添翼的你，早日构筑出自己的应用帝国，比心！

## 参考

- <https://mp.weixin.qq.com/s/Og9POTn4TDPoDOJNNkBxOA>
- <https://baike.baidu.com/item/JSON/2462549>
- <https://item.jd.com/10024550705540.html>