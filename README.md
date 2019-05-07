# ec-validate
数据表单校验

使用方式，引入 ec-validate-beta.js 即可使用 ecValidate 进行相应的校验。

## 1.api 

api|说明
---|---
check|校验若干字段，如果出现字段校验不通过，立即退出。返回出错的字段的提示信息。如果所有字段都通过校验，返回 undefined
checkAll|校验若干字段，返回所有出错的字段的提示信息。如果所有字段都通过校验，返回 undefined
extend|添加校验规则函数

## 2.check,checkAll

#### 2-1.使用说明
```JavaScript
    ecValidate.check([
        {
            data:data,
            rules:{
                ruleName:msg
            },
            filter:filterName
        }
    ])
```

#### 2-2.checkObj 参数说明

参数|说明|必填|类型|默认值|示例
---|---|---|---|---|---
data|待校验数据|是|string||
rules|校验规则对象|是|object||{ruleName:msg}(ruleName-规则名称，msg-提示信息)
filter|校验前处理的数据|否|string||
alias|错误信息位置（checkAll 独有参数）|是（checkAll 必传）|string|

## 3.extend

#### 3-1.使用说明

ecValidate.extend(ruleName,fn)

#### 3-2.参数说明

参数|说明|必填|类型|说明
---|---|---|---|---
ruleName|添加的规则名称|是|string|---
fn|规则的处理函数|是|function|(fn(val,msg) 至少要有 val,msg 这两个参数，而且顺序不能乱。如果有其他参数，需要放在两者之间)

#### 3-3.使用实例
```JavaScript
//添加扩展规则
ecValidate.extend('isPwd',function (val, msg) {
    if (!/^[a-zA-Z0-9.]+$/.test(val)) {
        return msg
    }
})
//客户端使用
let tips=ecValidate.check([
    {
        data:'@5626a',
        rules:{
            'isPwd':'请输入正确的密码格式'
        }
    }
]);
console.log(tips);
```

## 4.内置规则

规则名称|说明
----|----
isType|判断是否符合特定数据类型（string，number，boolean，null，function，array，object，symbol）
noType|判断是否不符合特定数据类型
isNoNull|是否为空
minLength|最小长度
maxLength|最大长度
isMobile|是否是手机号码格式
isTel|是否是固定电话
isEmail|是否是邮箱
isCard|是否是号码格式（身份证）
isNumber|是否是数字格式
hasNumber|是否包含数字格式
noNumber|是否不包含数字格式
isCount|是否是有效数值格式（多个小数点）
isChinese|是否是中文格式
hasChinese|是否包含中文
noChinese|是否不包含中文
isEnglish|是否是英文字母格式
hasEnglish|是否包含英文字母格式
noEnglish|是否不包含英文字母格式
isUpperEnglish|是否是大写英文字母格式
hasUpperEnglish|是否包含大写英文字母格式
noUpperEnglish|是否不包含大写英文字母格式
isLowerEnglish|是否是小写英文字母格式
hasLowerEnglish|是否包含小写英文字母格式
noLowerEnglish|是否不包含小写英文字母格式

## 5.filter可选参数

规则名称|说明
----|----
trim|校验之前去除前后空格
html|校验之前去除html标签

## 6.使用实例

./ec-validate-beta-demo.html

## LICENSE
MIT