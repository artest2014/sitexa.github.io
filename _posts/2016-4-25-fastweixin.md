---
layout: post
title: fastweixin - 快速搭建微信公众平台服务器
category: 'technology'
---

-   1.极其方便的实现微信公众平台服务端开发，2行代码完成服务器绑定，3行代码实现用户消息监听
-   2.支持多种web架构，无论你的项目使用springmvc还是servlet以及其他一切框架，都可以完美集成，API高度一致，使用者对架构差别无感知
-   3.完整封装微信消息收发报文，使用者无需研究理解微信提供的报文结构，入门极易
-   4.封装了绝大部分微信接口，还在不断完善

简单封装了所有与微信服务器交互的消息:文本消息、图片消息、图文消息等等.
提供了基于springmvc以及基于servlet框架的控制器，集成了微信服务器绑定、监听所有类型消息的方法.
使用时继承，重写即可，十分方便.

-   v1.2.0开始支持高级接口的API，https请求基于org.apache.httpcomponents 4.3.X，json解析基于fastjson 1.1.X
框架中提供MenuAPI、CustomAPI、QrcodeAPI、UserAPI、MediaAPI、OauthAPI用于实现所有高级接口功能，使用极其简单
内部实现token过期自动刷新，不用再关注token细节

-   v1.2.6开始支持微信消息安全模式，但由于jdk的限制，导致想使用安全模式，必须修改jdk内部的jar包
    -   [JCE无限制权限策略文件JDK7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
    -   [JCE无限制权限策略文件JDK8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)
    -   下载后解压，可以看到local_policy.jar和US_export_policy.jar以及readme.txt
    -   如果安装了JRE，将两个jar文件放到%JRE_HOME%\lib\security目录下覆盖原来的文件
    -   如果安装了JDK，将两个jar文件放到%JDK_HOME%\jre\lib\security目录下覆盖原来文件

-   v1.3.0重构了微信消息接收控制器，将WeixinSupport类完全独立抽象出来，不再依赖web框架.所以WeixinServletSupport类不再兼容之前的版本，具体使用方法如下:

## 基于springmvc项目的集成方法

    @RestController
    @RequestMapping("/weixin")
    public class WeixinController extends WeixinControllerSupport {
            private static final Logger log = LoggerFactory.getLogger(WeixinController.class);
            private static final String TOKEN = "myToken";
            //设置TOKEN，用于绑定微信服务器
            @Override
            protected String getToken() {
                return TOKEN;
            }
            //使用安全模式时设置：APPID
            //不再强制重写，有加密需要时自行重写该方法
            @Override
            protected String getAppId() {
                return null;
            }
            //使用安全模式时设置：密钥
            //不再强制重写，有加密需要时自行重写该方法
            @Override
            protected String getAESKey() {
                return null;
            }
            //重写父类方法，处理对应的微信消息
            @Override
            protected BaseMsg handleTextMsg(TextReqMsg msg) {
                String content = msg.getContent();
                log.debug("用户发送到服务器的内容:{}", content);
                return new TextMsg("服务器回复用户消息!");
            }
            /*1.1版本新增，重写父类方法，加入自定义微信消息处理器
             *不是必须的，上面的方法是统一处理所有的文本消息，如果业务觉复杂，上面的会显得比较乱
             *这个机制就是为了应对这种情况，每个MessageHandle就是一个业务，只处理指定的那部分消息
             */
            @Override
            protected List<MessageHandle> initMessageHandles() {
                    List<MessageHandle> handles = new ArrayList<MessageHandle>();
                    handles.add(new MyMessageHandle());
                    return handles;
            }
            //1.1版本新增，重写父类方法，加入自定义微信事件处理器，同上
            @Override
            protected List<EventHandle> initEventHandles() {
                    List<EventHandle> handles = new ArrayList<EventHandle>();
                    handles.add(new MyEventHandle());
                    return handles;
            }
    }
    
## 基于servlet项目的集成方法

    public class WeixinServlet extends WeixinServletSupport {
            @Override
            protected WeixinSupport getWeixinSupport() {
                    return new MyServletWeixinSupport();
            }
    }
    //用户自行实现的微信消息收发处理器
    public class MyServletWeixinSupport extends WeixinSupport {
        private static final Logger log = LoggerFactory.getLogger(MyServletWeixinSupport.class);
        @Override
        protected String getToken() {
            return "myToken";
        }
        @Override
        protected BaseMsg handleTextMsg(TextReqMsg msg) {
            String content = msg.getContent();
            log.debug("用户发送到服务器的内容:{}", content);
            return new TextMsg("服务器回复用户消息!");
        }
    }
    
web.xml配置

    <servlet>
        <servlet-name>weixin</servlet-name>
        <servlet-class>xxx.xxx.WeixinServlet</servlet-class>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>weixin</servlet-name>
        <url-pattern>/weixin</url-pattern>
    </servlet-mapping>
    
## 基于Jfinal框架项目的集成方法

    public class MyJfinalController extends Controller {
        //用户自行实现的消息处理器
        private WeixinSupport support = new MyServletWeixinSupport();
        public void index() {
                HttpServletRequest request = getRequest();
                log.debug("method:{}", request.getMethod());
                //绑定微信服务器
                if ("GET".equalsIgnoreCase(request.getMethod().toUpperCase())) {
                    support.bindServer(request, getResponse());
                    renderNull();
                } else {
                    //处理消息
                    renderText(support.processRequest(request), "text/xml");
                }
            }
    }
    
## Maven 项目引入

    <dependency>
        <groupId>com.github.sd4324530</groupId>
        <artifactId>fastweixin</artifactId>
        <version>1.3.8</version>
    </dependency>
    
