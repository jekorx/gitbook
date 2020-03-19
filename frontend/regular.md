# 正则表达式

#### 常用正则表达式

```js
// 手机号校验
/^1[3456789]\d{9}$/

// 邮箱校验
/^\w+((-\w+)|(\.\w+))*@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/

// 身份证号校验
/^[1-9]\d{5}(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/
```