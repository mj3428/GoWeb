# 内容展示
## 模板引擎
两种极端类型的模板：I:无逻辑模板引擎（logic-less template engine）II:嵌入逻辑的模板引擎（embedded logic template engine）
在实际中，绝大多数有用的模板引擎都会介于以上两种理想的模板之间。Go标注库提供的模板引擎功能大部分都定义在了text/template库当中，
而小部分与HTML相关的功能定义在了html/template库里面。两个库相辅相成，可以当成无逻辑模板引擎使用，与此同时，Go也提供了足够多的嵌入式
模板引擎特性，使这个模板引擎用起来既有趣又强大。