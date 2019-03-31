#### http协议整理
- 腾讯面试的时候问到了一个http客户端发送一万请求的问题， 涉及到了http1.1 和http2.0 才发现自己对http2一无所知， 故作一个整理
- [谷歌developer解释http2](https://developers.google.com/web/fundamentals/performance/http2/?hl=zh-cn)
##### http2小结
- 基于2进制的协议实现， 让协议处理变得更加强大灵活， 同时保持了上层的httpapi不变
- 设计目标可以认为是尽量提升性能， 核心是使用了多路复用的流， 在一个tcp连接上处理多个请求
- 流的一些特点， 可以拆分数据帧然后重组， 可以设置优先级和依赖关系
- 其他， 服务端的主动请求和标头压缩（复用）
##### http 里面流的解析
- 腾讯面试的时候问到http 协议里是处理处理粘包问题的， 当时经过引导的作答时根据content length, 回头在知乎上查这个问题， 发现
粘包这个词属于中式术语， 正确的理解应该是如何在基于流的协议上实现基于message的协议。
- 参考知乎回答 [解析 http 协议是否要处理粘包？DCjanus的回答 - 知乎](https://www.zhihu.com/question/24598268/answer/625136503)
