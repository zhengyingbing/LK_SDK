# SDK开发规范
## 一 开发环境
为了项目维护起来更方便、代码可读性更强、同事之间接手项目更快速以及团队的开发更规范，根据一年来的SDK开发经验，总结此文。不管是APP开发还是SDK开发，一个团队拥有相同的开发环境是很有必要的。所以我们首先需要统一IDE版本、JDK版本、Gradle版本、三方库版本、编码格式等等。
另外需要注意，SDK开发讲究轻量、稳定、便捷，所以我们要尽量少的引用三方库，所有的功能尽可能通过同一个类进行调用，更多的工作是考虑稳定、适配和性能。
## 二 AS规范
1.编写完java、xml后一定记得格式化（ctrl + shift + F）

2.java文件编写完成后，记得删除无效代码和引用，尽可能减少警告出现（ctrl + shift + O）

3.尽量减少jar,aar的引用，采用maven引用的方式

4.so库调用时需要增加arm架构64位cpu的版本，googleplay强制要求

## 三 命名规范
代码中避免使用英文+拼音混合方式。对于专业性较强的名称给予完整命名并添加详细注释，不可随意缩写。

3.1 包名
公司的SDK项目分为基础OKSDK基工程SDK、网络SDK、权限SDK、OKSDK工程SDK、海外自主登录SDK、海外渠道登录SDK、
国内自主登录SDK、国内渠道登录SDK、海外支付SDK（google）、海外支付SDK（onestore）...、国内支付SDK（目前集成6中支付）

包命名格式：顶级域名+公司名+业务名（功能名）

目前OKSDK基工程包名：com.oksdk.helper

网络SDK：com.linekong.http

权限SDK：com.linekong.permissons

OKSDK：com.oksdk.channel

海外自主登录SDK：com.linekong.abroad

国内自主登录SDK：com.internal.sdk

海外支付SDK：com.linekong.pay

3.2 类名
UpperCamelCase大驼峰命名法
<table>
        <tr>
            <th>类</th>
            <th>描述</th>
            <th>举例</th>
        </tr>
        <tr>
            <th>Activity</th>
            <th>Activity为后缀标识</th>
            <th>LoginActivity</th>
        </tr>
        <tr>
            <th>Adapter</th>
            <th>Adapter为后缀标识</th>
            <th>AccountAdapter</th>
        </tr>
        <tr>
            <th>工具类</th>
            <th>Utils或Manager</th>
            <th>线程池管理类ThreadPoolManager，日志工具LogUtils</th>
        </tr>
         <tr>
            <th>数据库类</th>
            <th>DBHelper后缀</th>
            <th>AccountDBHelper</th>
        </tr>
         <tr>
            <th>Service类</th>
            <th>以Service为后缀</th>
            <th>TimeService</th>
        </tr>
         <tr>
            <th>基类</th>
            <th>以Base开头</th>
            <th>BaseActivity</th>
        </tr>
    </table>


3.3 方法名

lowerCamelCase风格，不细说

3.4常量名

全部字母大写，单词用下划线隔开，必须使用static final修饰。哪些属性定义为常量？
在SDK中，可定义常量的属性有：网络返回错误码、加密key、网络请求时间参数、偏好保存文件的key、intent传递的参数key、
arguement参数的key、注册协议地址

3.5非常量名

lowerCamelCase 风格，不细说

3.6参数名

lowerCamelCase 风格，在SDK中传递多个参数的格式是：
method(context，param1,param2..,callback)

3.7局部变量名

lowerCamelCase 风格，不细说

3.8临时变量名
整型：i,j,k,m,n
字符型：a,b,c,d,e

3.9类型变量名
单个大写字母（可以跟一个数字），T、T2

## 四 代码样式规范
4.1 大括号使用
左大括号与前面的代码位于同一行。如果在条件语句中省略大括号，则将整个语句放在同一行。
正确样式：
if(isLogin){
  pay();
}

if(isLogin) pay();
错误样式：
if(isLogin)
  pay();
4.2 编写简单的方法
  如果一个方法中代码超出40行，则进行合理拆分
4.3 swtich..case..使用
  如果在case中代码超过6行，则将代码单独放到一个方法中
4.4 类中代码编写顺序
有的类中有数百行代码，使用统一的顺序，可以提高代码的可读性，推荐顺序如下：
（1）常量

 (2) 成员变量
 
（3）构造函数

（4）重写和回调

 (5) 公有函数
 
（6）私有函数

（7）内部类

（8）接口

例如：
```java
public class LKAccountActivity extends BaseActivity implements ILoginResult{
  private static final String TAG = "lk_lkaccount";
  
  private UserInfo mUserInfo;
  @Override
  public void onCreate(){
    ...
  }
  
  public void getKeyHash(){
    ...
  }
  private void login(){
    ...
  }
  static class LKAccoun
}
```

## 合理的创建标题，有助于目录的生成
## 如何改变文本的样式
## 如何插入一段漂亮的代码片

## 生成一个适合你的列表
