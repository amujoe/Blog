# 有什么疑问：


- Q：什么时机弹出隐私协议的弹窗？
- A：如果是被动触发；api 是在api 调用时机触发；组件是在组件初始化时候会触发；
- A：如果是主动触发；根据返回的状态，自主调用弹框


- Q： N多个Api 接口需要授权，每个在调用之前都需要授权吗？
- A：不需要每个都授权；只需要授权一次；mp后天有更新后，会再次弹窗；


- Q：用户拒绝了怎么办？
- A：需要有兼容方案，让用户体验正常