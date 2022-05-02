# problem
#该文档记录在开发过程中遇到的问题，以及解决方案
1、 Resolved [org.springframework.web.HttpMediaTypeNotSupportedException: Content type 'application/x-www-form-urlencoded;charset=UTF-8' not supported]
上述异常，在springboot项目中，遇到。解决方案：前端传递参数并非json,而后端用 @RequestBody 注解将前端数据映射到对象中，去掉该注解即可。

2、Circular view path [error]: would dispatch back to the current handler URL [/error] again. Check your ViewResolver setup! (Hint: This may be the result of an unspecified view, due to default view name generation.)
springboot项目异常，原因：整合jsp时没有指定前缀后缀。解决方案，在application.yml中，加入
  view:
      suffix: .jsp
      prefix: /
3、If you want an embedded database (H2, HSQL or Derby), please put it on the classpath.
	If you have database settings to be loaded from a particular profile you may need to activate it (no profiles are currently active).
  重新打包，删除target包
4、springboot集成druid登陆mysql发生errorCode 1045， state 28000错误
      1、mysql用户密码错误
      2、mysql用户权限
      3、我出现的情况是在cmd命令行下能够正常登陆，但是在项目中配置的参数是：
      url：jdbc：mysql：//loca
      username：root
      password：0000
会出现java.sql.SQLException： Access denied for user 'root'@'localhost' (using password： YES)， 此时给0000加个单引号变为'0000'则登陆成功，根本原因还是因为密码错误。
yml文件上对于纯数字类型的密码需要加引号，如果是包含字母的就不需要。
