# SDK开发规范
## 一 开发环境

为了项目维护起来更方便、代码可读性更强、同事之间接手项目更快速以及团队的开发更规范，根据我一年来的SDK开发经验，总结此文。不管是APP开发还是SDK开发，一个团队拥有相同的开发环境是很有必要的。所以我们首先需要统一IDE版本、JDK版本、Gradle版本、三方库版本、编码格式等等。

另外需要注意，SDK开发注重轻量、稳定、便捷，所以我们要尽量少的引用三方库，所有的功能尽可能通过同一个类进行调用，更多的工作是保证稳定、适配和性能。

## 二 AS规范

        2.1 编写完java、xml后一定记得格式化（ctrl + shift + F）

        2.2 java文件编写完成后，记得删除无效代码和引用，尽可能减少警告出现（ctrl + shift + O）

        2.3 尽量减少jar,aar的引用，采用maven引用的方式

        2.4so库调用时需要增加arm架构64位cpu的版本，googleplay强制要求

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
        单个大写字母（可以跟一个数字）：T,T2

## 四 代码样式规范
4.1 大括号使用

        左大括号与前面的代码位于同一行。如果在条件语句中省略大括号，则将整个语句放在同一行。
        正确样式：
```java
if(isLogin){
  pay();
}
```

        或
```java
if(isLogin) pay();
```

        错误样式：
```java
if(isLogin)
  pay();
```

4.2 编写简单的方法

          如果一个方法中代码超出40行，则进行合理拆分
  
4.3 ``` swtich..case.. ```使用

          如果在case中代码超过6行，则将代码单独放到一个方法中
  
4.4 类中代码编写顺序

        Activity或Fragment中重写的函数按生命周期排序，养成良好编码习惯。

        有的类中有数百行代码，使用统一的顺序，可以提高代码的可读性，推荐顺序如下：

        （1）常量

        （2）成员变量
 
        （3）构造函数

        （4）重写和回调

        （5）公有函数
 
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
  static class MyHandler{
    ...
  }
}
```

4.5函数中的参数排序

        Context和回调函数是最常用的参数，在Android中一般以Context参数做开头，回调参数做结尾，举个例子：

```java
public void login(Context context, String name, String pwd, LoginCallback callback){
        ...
}
```

4.6 字符串常量的命名和值

        在SDK开发中，很多类都用到了键值对函数，比如SharePreferences、Bundle、Intent等，为了避免和接入方引起不必要的重复和冲突，我们要将这些属性定义为static final字段，所有key值字母均大写，单词之间用下划线隔开，key对应的值以包名为前缀。举例：

```java
public static final String PREF_ISLOGIN = "com.linekong.abroad.PREF_ISLOGIN";
```

4.7 Activity与Fragment的跳转传值

        在Android中Activity与Fragment的跳转和传值有多种方式，为了统一代码规范。建议使用AS提供的相关Live Templates。跳转Activity我们只需在目标Activity中输入starter即可自动生成跳转方法。同理，在目标Fragment中内部输入newInstance，即可自动生成跳转方法。

4.8 代码行长限制

        每行不超过100个字符（AS右侧竖线标识行宽末尾），网址链接除外。处理行长方式：将参数提成一个变量（优先），或者使用换行符换行。

4.9 操作符换行

        略

4.10 函数链换行，链式调用换行

        略

4.11 多参数换行

        略

## 五 资源文件规范

5.1 动画资源文件(anim/和animator/)

        略

5.2 颜色资源文件(color/)

        选择器文件命名：sel_{模块名}_{逻辑名}_{组件类型}.xml，{}中为可选

        举例： sel_lkaccount_login_btn.xml, sel_common_cancel_btn.xml

5.3 图片资源文件（drawable/和mipmap/）

        res/drawable/ 中存放位图文件（.png,.jpg,.9.png,.gif,.xml）

        res/mipmap/ 中存放不同密度的启动图标

5.4 布局资源文件(layout/)

        命名规则：类型_模块_逻辑.xml

        举例：activity_lkaccount_login.xml

        view_common_loading.xml

        dialog_paymain_pay.xml

5.5 菜单资源文件（menu/）

        略

5.6 values资源文件（values/）

        values/文件夹下的文件都以s结尾，这里注意起作用的不是文件名而是<resources>标签下的各种标签，比如<style>决定样式，<color>决定颜色。
        
        在sdk开发中，为了更好的开发和维护项目，我们最好单独创建此类资源文件。
        
        举例：style_lkaccount_abroad.xml

        color_internal_pay.xml
      
5.6.1 color.xml下的排版格式及资源命名

        我们定义colors的属性时，首先定义此项目所有的基色，然后用注释拆分个模块的color值，尽量以相近的颜色单词来命名color值，有效避免重复定义argb值。
        错误做法举例：
    
    ```java
      <resources>
      <color name="button_foreground">#FFFFFF</color>
      <color name="button_background">#2A91BD</color>
      <color name="comment_background_inactive">#5F5F5F</color>
    ```
    
正确做法举例：
    ```java
      <resources>
      <!-- basic colors -->
      <color name="white">#FFFFFF</color>
      <color name="gray_light">#dbdbdb</color>
      <color name="black">#333333</color>
      <!-- lkaccount colors -->
      <color name="green">#27D34D</color>     
              ...
    ```
5.6.2 string.xml 

        命名规则：SDK功能相关名_模块名_逻辑名_组件类型

        举例：lkaccount_login_pwd_hint
        internalpay_dialog_cancel_btn
        
5.6.3 dimens.xml

     与colors相似，注意排序和命名
     举例：
     
```java
   <resources>
        <!-- font sizes -->
        <dimen name="sp_12">12sp</dimen>
        <dimen name="sp_15">15sp</dimen>
        <dimen name="sp_18">18sp</dimen>
        <dimen name="sp_22">22sp</dimen>

        <!-- views sizes -->
        <dimen name="dp_10">10dp</dimen>
        <dimen name="dp_14">14dp</dimen>
        <dimen name="dp_24">24dp</dimen>
        <dimen name="dp_32">32dp</dimen>
    
        <!-- buttons size -->
        <dimen name="button_dp_32">32dp</dimen>
        <dimen name="button_dp_40">40dp</dimen>
        <dimen name="button_dp_60">60dp</dimen>
   </resources>    
```

5.6.4 styles.xml

    命名规则：大驼峰命名
    举例：
    ```java
        <style name="Base">
        <item name="android:background">@color/white</item>
        </style>
        <style name="Base.Text">
        <item name="android:textSize">@dimen/dp_14</item>
        </style>
        <style name="Base.Text.EditText">
        <item name="android:textColorHint">@color/gray_light</item>
        </style>
    ```
    
5.7 layout中id命名：

            类类型名开头，组件类型名结尾，
            举例：activity_login_btn
            fragment_login_pwd_icon

## 六 注释规范

           类注释，在AS中添加LiveTemplete模板，进入 Settings -> Editor -> File and Code Templates -> Includes -> File Header，输入
```java
   /**
    * <pre>
    *     author : zyb
    *     e-mail : 23844078@qq.com
    *     time   : ${YEAR}/${MONTH}/${DAY}
    *     desc   :
    *     version: 1.0
    * </pre>
    */
```

        方法注释，使用多行注释
        代码块注释，使用单行注释//  或 /* ... */

        其他注释，在未实现的或者需要修正的方法上添加// 或者 //FIXME标签添加注释，可以快速定位
## 七 其他规范

          7.1 提供统一的数据入口，代码更容易维护。比如初始化、登录、 登出、绑定、用户中心都放在LKAccount类中操作
          7.2 多用组合，少用继承
          7.3 抽取必要的工具类
          7.4 尽可能使用局部变量，尽量少的定义静态常量
          7.5 当有过个构造函数或同名函数，应该顺序出现，不要夹杂其他函数
          7.6 尽量减少定义变量的次数
          错误：
  ```java
  for(int i=0; i < list.size(); i++){
        ...
  }
  ```
          正确：
  ```java
  for(int i=0, size = list.size(); i < size; i++){
        ...
  }
  ```
          7.7 尽量采用懒加载策略
            错误：
  ```java
  String str = "abc";
  if (i == 1){
      list.add(str);
  }
  ```
          正确：
  ```java
  if (i == 1){
      String str = "abc";
      list.add(str);
  }
  ```
          7.8 不要在循环中使用try..catch，try..catch应该放在循环外部
          7.9 使用AS自带的Lint来优化代码结构

