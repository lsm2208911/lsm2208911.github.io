---
layout:     post
title:      "springboot Controller 传参总结"
subtitle:   "@RequestPara 与 @RequestBody用法"
date:       2019-11-19
author:     "无力去闹"
header-img: "img/post-bg-js-version.jpg"
tags:
    - springboot
---


# spring boot接收各种参数总结：
## 1. 参数为简单对象（参数为基本类型时）
``` java
//实体类
@Setter
@Getter
public Class User{
  private String name;

  private Integer age;
}
```
### 使用Json进行数据传输
前端：
``` js
var param = {name:zhsnasn,age:18} //构造一个js对象
$.ajax({
    url : '/getUser',
    type : 'post',
    data : JSON.stringify(param),
    contentType : "application/json;charset=utf-8",//contentType重要，告诉后端传入的参数为json格式
    success:function (resp) {
       //.....
    },
    error:function () {
      //....
    }
});
```
后台
``` java
//controller
public Class UserController{
  @PostMapping("/getUser")
  @ResponseBody
  //@RequestBody作用为：根据请求头的contentBody自动解析请求体并绑定到方法参数上
  public AjaxResult getUser(@RequestBody User param){
      //....
  }
}
```
### 使用表单进行数据传输
``` js
var param = {name:zhsnasn,age:18} //构造一个js对象
//post提交contentType默认为 "application/x-www-form-urlencoded"
$.post("/addUser",param,function(resp){
  //.....
});
```
后台
``` java
//controller
public Class UserController{
  @PostMapping("/addUser")
  @ResponseBody
  //不在需要@RequestBody
  public AjaxResult addUser(User param){
      //....
  }
}
```
## 2. 复杂对象 一般使用json传输
``` java
//实体类
@Setter
@Getter
public Class Menu{
  private Long id;

  private String menuName;
}

@Setter
@Getter
public Class Organization{
  private Long id;

  private String orgName;
}

@Setter
@Getter
public Class User{
  private String userName;

  private Integer age;

  private List<Menu> menus;

  private Organization org;
}
```
前台
``` js
var param = {name:zhsnasn,age:18} //构造一个js对象
var menus = [], menu1 = {id:1,menuName='menu1'}, menu2 = {id:2,menuName='menu2'}, org={id:1,orgName:'orgName1'};
menus.push(menu1);
menus.push(menu2);
param.menus = menus;
param.org = org;
$.ajax({
    url : '/addUser',
    type : 'post',
    data : JSON.stringify(param),
    contentType : "application/json;charset=utf-8",//contentType重要，告诉后端传入的参数为json格式
    success:function (resp) {
       //.....
    },
    error:function () {
      //....
    }
});
```
后台
``` java
//controller
public Class UserController{
  @PostMapping("/addUser")
  @ResponseBody
  public AjaxResult addUser(@RequestBody User param){
      //....
  }
}
```
## 3. 当Controller中方法参数要使用数组、列表或者Map进行接收时，可以使用@RequestParam注解。
前台
```js
var dataList = [1,2,3,4]
$.ajax({
    url:"/addUserGroup",
    type:'post',
    data:{ids:dataList},
    traditional:true,
    success:function (resp) {
      //....
        }
    }
})
```
后台
``` java
//controller
public Class UserController{
  @PostMapping("/addUserGroup")
  @ResponseBody
  public AjaxResult addUser(@RequestParam("ids") List<Integer> stringList){
      //....
  }
}
```
参考：[spring.io](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html)