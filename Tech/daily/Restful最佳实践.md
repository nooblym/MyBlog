# Restful最佳实践

[TOC]

REST风格更适用于以数据为中心的架构，而非以计算为中心的架构

### 请求 = 动词 + 宾语

**RESTful 的核心思想就是，客户端发出的数据操作指令都是"动词 + 宾语"的结构**

1. 动作

   动词通常就是五种 HTTP 方法

   - GET：读取（Read）
   - POST：新建（Create）
   - PUT：更新（Update）
   - PATCH：更新（Update），通常是部分更新
   - DELETE：删除（Delete）

2. URI

   宾语就是 API 的 URI，是 HTTP 动词作用的对象。它应该是名词，不能是动词。比如，`/articles`这个 URL 就是正确的，而`getXXX,putXXX...`都是不符合规范的

3. 属性

4. url带版本信息

5. 必须的信息写在url中，可选的作为属性信息附加上去

   `https://api.domain.com/v1/user/{xxx}?`使用正确吗

   `https://api.domain.com/v1/user/{xxx}/xxx?`使用正确吗

   一个好的RESTfulAPI必须使用HTTPS作为前缀

6. url中表示的名词比属性中表示的要强，所以获取的信息应该也比属性要丰富

7. 尽量减少对第三方开发人员的随意约束---不要在接口中添加默认的约束条件

状态码



## 参考项目

+ https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md