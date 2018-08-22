# 第四篇 如何造一个类RN轮子

> RN全称(React Native),是一个跨平台的移动端类Native开发的框架.

## 1. RN存在哪些不足?

* 包体积大小的问题;
* List性能差的问题;
* 不同平台API的差异化问题;

## 2. 如何设计一个类RN?

仅仅是一种思考方式:

* 需要考虑对齐RN的语法和API,让开发者尽量没有切换成本;
* 需要考虑架构分层,横向扩展各类框架;
* 在没有底层内核的情况下,考虑如何提高性能;
* 需要抹平所有组件和模块在不同端的差异,且能够支持降级为H5,一套代码,多端同步.
* 需要考虑整套解决方案,不仅包含发布系统等;

## 3. 需要思考以下维度

* 包大小: 如何控制
* List性能: 需要考虑在终端构建虚拟Node树+特定的diff算法,在List滑动时做到极致的复用;
* List滑动性能问题: RN滑动时内存上涨比较明显;
* 解决首次启动到首字的速度优化
* 二次启动到首字的速度,是否考虑在V8做缓存;
* 线程模型:考虑排版和UI线程的分离;
* 系统的兼容性覆盖度;
* 提升so加载的成功率;
* 抹平多端的差异;
* 机型兼容性问题,比如文字截断等;
* 前终端通信方式的改进:通过原来的注册表和json串协议改成直接函数调用,相关的堆栈信息由前端打到终端;
* 动画方案上,目前由前端驱动存在性能瓶颈,RN原生动画,在执行动画时,如果同时又有大量页面render,就一定会卡
* 手势系统:不管前端有没有绑定touch事件,只要触发touch就会发消息,消息通道被严重阻塞;
* 前端打包方式: 默认不支持拆分打包,介入都需要自己做拆包,可以考虑webpack来拆包;
* 发布系统:这是框架升级为解决方案关键的一步.

## 4. 需要考虑工具链,提升开发体验

* 是否考虑建设打包平台:自动上传CDN,生成即可安装包体验的二维码
* 能否进行服务端一键打包;
* 需要考虑发布系统,通过配置规则就可动态更新;

## 5. 一些更长远的考虑

* 上层无缝兼容主流web框架,并提供可以简单扩展的js框架的接口;
* 有更多的辅助工具,调试工具、在线IDE,组件库等;

## 6. 考虑业务如何平滑迁移

* 纯Native如何能够迁移类RN;
* H5业务如何快速迁移类RN;
* hybrid如何快速迁移类RN.
...

发挥你的想象力