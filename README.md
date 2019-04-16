### Mblog 开源Java博客系统, 支持多用户, 支持切换主题

[![Author](https://img.shields.io/badge/author-landy-green.svg?style=flat-square)](http://mtons.com)
[![JDK](https://img.shields.io/badge/jdk-1.8-green.svg?style=flat-square)](#)
[![Release](https://img.shields.io/github/release/langhsu/mblog.svg?style=flat-square)](https://github.com/langhsu/mblog)
[![license](https://img.shields.io/badge/license-GPL--3.0-green.svg)](https://github.com/langhsu/mblog/blob/master/LICENSE)
[![Docker](https://img.shields.io/docker/automated/langhsu/mblog.svg?style=flat-square)](https://hub.docker.com/r/langhsu/mblog)
[![QQ群](https://img.shields.io/badge/chat-Mtons-green.svg)](https://jq.qq.com/?_wv=1027&k=521CRdF)

### 技术选型：

* JDK8
* MySQL
* Spring-boot
* Spring-data-jpa
* Shiro
* Lombok
* Freemarker
* Bootstrap
* SeaJs


MySQL    端口:3306
用户名:root
密码:  空



### 启动：
 - main方法运行
 ```xml
 配置：src/main/resources/application-mysql.yml (数据库账号密码)、新建db_mblog的数据库
 运行：src/main/java/com/mtons/mblog/BootApplication
 访问：http://localhost:8080/
 后台：http://localhost:8080/admin
 账号：默认管理员账号为 admin/12345
 
 TIPS: 
 如遇到启动失败/切换环境变量后启动失败的,请先maven clean后再尝试启动
 IDE得装lombok插件
```

- 文档: [说明文档](https://langhsu.github.io/mblog/#/)
- 官网: [官网地址](http://www.mtons.com)
- QQ交流群：378433412
    
### 版本(3.5)更新内容：
    1. 文件存储目录可配置, 见 site.location, 默认为 user.dir
    2. 支持在${site.location}/storage/templates 目录下扩展自己的主题(${site.location}具体位置见启动日志)
    3. 后台未配置对应第三方登录信息时, 前端不显示对应的按钮
    4. 模板优化
    5. 后台配置主题改为自动从目录中加载
    6. 新增markdown编辑器, 可在后台选择tinymce/markdown
    
### 版本(3.0)更新内容：
    1. 新增开关控制(注册开关, 发文开关, 评论开发)
    2. 后台重写, 替换了所有后台页面功能更完善
    3. 上传图片添加更多支持(本地/又拍云/阿里云/七牛云), 详情见后台系统配置
    4. 升级为spring-boot2
    5. 调整模板静态资源引用,方便扩展
    6. 表名调整, 旧版本升级时请自行在数据库重命名, 详情见change.log
    7. 重写了config(改为options), 可在applicaiton.yaml设置默认配置, 启动后将以options中配置为准
    8. 支持后台设置主题
    9. 去除了本地文件上传目录配置, 改为自动取项目运行目录(会在jar同级目录生成storeage和indexes目录)
    10. 替换表单验证插件, 评论表情改为颜文字
    11. 我的主页和Ta人主页合并
    12. 优化了图片裁剪功能
    13. 支持Docker, 详情见 https://hub.docker.com/r/langhsu/mblog
    14. 邮件服务后台可配
    15. 新增标签页
    16. 新增注册邮箱验证开关(需要手动删除之前的 mto_security_code 表)
        
### 图片演示 
![首页](https://images.gitee.com/uploads/images/2019/0125/142627_fcd67bfd_116277.jpeg "前台首页.jpg")
![文章](https://images.gitee.com/uploads/images/2019/0125/142647_328aa3d7_116277.jpeg "文章阅读.jpg")
![后台](https://images.gitee.com/uploads/images/2019/0125/142704_cca6a479_116277.jpeg "后台首页.jpg")
![后台文章管理](https://images.gitee.com/uploads/images/2019/0125/142725_3754efbf_116277.jpeg "后台文章编辑.jpg")

图片来自@weian豆丁

### 这些用户在使用mblog(如需要在此展示您的博客请联系作者)：
[https://www.lyp82nlf.com/](https://www.lyp82nlf.com/)

[http://www.outshine.cn/](http://www.outshine.cn/)

[http://www.jiangxindc.com](http://www.jiangxindc.com)

[http://www.mhtclub.com/](http://www.mhtclub.com/)

[http://www.maocaoying.com/](http://www.maocaoying.com/)



  1.发送邮件:配置
        String mailHost = "smtp.qq.com";   //配置用什么邮箱;
        String mailUsername = "764569359@qq.com"; //发送者QQ号码;
        String mailPassowrd = "qmayecvrprulbcfh"; //配置授权码;
        
  2.邮箱是否开启:差别
        register_email_validate: true/false
        true:会进行邮箱注册;
        false：不会进行邮箱注册;
        
  3.Jpa方法(增删改查):
        接口实现类:public interface PostAttributeRepository extends JpaRepository<PostAttribute, Long>, JpaSpecificationExecutor<PostAttribute{}             
        可以添加方法:
            public interface PostAttributeRepository extends JpaRepository<PostAttribute, Long>, JpaSpecificationExecutor<PostAttribute>
            {
                   Iterable<T> findAll(Sort var1);
                   Page<T> findAll(Pageable var1);
             }
        接口内容:
             public interface JpaRepository<T, ID> extends PagingAndSortingRepository<T, ID>, QueryByExampleExecutor<T>
                 {
                 List<T> findAll();
                 List<T> findAll(Sort var1);
                 List<T> findAllById(Iterable<ID> var1);
                 <S extends T> List<S> saveAll(Iterable<S> var1);
                 void flush();
                 <S extends T> S saveAndFlush(S var1);
                 void deleteInBatch(Iterable<T> var1);
                 void deleteAllInBatch();
                 T getOne(ID var1);
                 <S extends T> List<S> findAll(Example<S> var1);
                 <S extends T> List<S> findAll(Example<S> var1, Sort var2);
                    }
                    
   4.登陆
             页面:/login
             后台:LoginController.java
             方法名:/login
             1.登陆时判断:用户名和密码是否为空
             2.进入后台,并进行查询数据库
             3.登陆成功，插入字段登录时间、状态到数据库
                 
  
   页面跳转流程:
              5.1:
               interface Views(接口):页面配置接口
                Sql表:
                          mto_user:用户表
                          mto_channel:导航表
                          mto_options:网站配置表
                          shiro_permission:后台配置权限表
                          shiro_role:设置角色权限表
                          mto_post:文章全部信息表
                          mto_post_attribute:文章内容表
                          mto_comment：评论内容表
                          mto_favorite:收藏文章表
                          mto_tag：文章标签表
                          mto_options:分享内容表
                          
                          
   导航页面:
                          对应Controller： ChannelController(博客、随笔、分享)
                          方法:/channel/{id}
                          参数:id
                          id类别:
                          2:博客
                          3：随笔
                          4：分享
                          标签 对应Controller：:TagController(标签)
                          方法:/tags
                          搜素方法:
                          对应Controller： SearchController
                          对应方法:/search
                          参数:(String kw, ModelMap model)
                          写文章:
                          对应Controller：PostController
                          方法:list
                          参数:(String title, ModelMapmodel,HttpServletRequest request)
                          编辑文章:
                          方法：toUpdate
                          参数:Long id, ModelMap model
                          更新文章:
                          方法:subUpdate
                          参数:PostVO post(实体类)
                          删除文章:
                          方法:delete
                          参数:id
   个人主页面:
                   编辑资料:
                       更新基础信息:
                           对应Controller：SettingsController 
                           @PostMapping(value = "/profile")
                           方法:updateProfile
                           参数:String name, String signature, ModelMap model
                           调用Sql语句:userService.update(user)
                       更新邮箱信息:
                            @PostMapping(value = "/email")
                            方法:updateEmail
                            参数:String email, String code, ModelMap model
                            调用Sql语句:userService.updateEmail
                       更新密码信息:
                            @PostMapping(value = "/password")
                            方法:updatePassword 
                            参数:String oldPassword, String password, ModelMap model
                            调用Sql: userService.updatePassword
                       更新图片信息:
                            @PostMapping("/avatar")
                            方法:UploadResult
                            参数:MultipartFile file(图片类型)
                            调用Sql:userService.updateAvatar  
                            
                            
   首页:
                       登陆页面:
                          页面跳转:@GetMapping(value = "/login")
                             public String view() 
                                 {
                            	return view(Views.LOGIN);
                            	            }
                             提交登陆:@PostMapping(value = "/login")
                             Controller：LoginController
                                   方法：login
                                   参数:String username,String password,@RequestParam(value = "rememberMe",defaultValue = "0") Boolean rememberMe,ModelMap model
                                   找回密码:
                                             Controller:ForgotController
                                             @PostMapping("/forgot")
                                             方法:reset
                                             参数:String email, String code, String password, ModelMap model
                                             调用Sql:serService.getByEmail
                                    注册页面:
                                              Controller:RegisterController
                                              @PostMapping("/register")
                                              方法:register()
                                              参数:UserVO post, HttpServletRequest request, ModelMap model
                                    退出操作:
                                               Controller:LogoutController
                                               @RequestMapping("/logout")
                                               方法:logout()
                                               参数:HttpServletResponse response
                                    页面跳转(重定向):
                                               返回值:return Views.REDIRECT_INDEX;
                                               重定向:REDIRECT_INDEX = "redirect:/index" 
                                               
   后台管理系统:
                  栏目管理:
                       查询全部栏目:
                         Controller:ChannelController
                         @RequestMapping("/list")
                         方法:list
                         调用Sql:channelService.findAll
                       查询单个栏目:
                          @RequestMapping("/view")
                          方法:view
                          参数:Integer id, ModelMap model
                       更新栏目信息:
                          @RequestMapping("/update")
                          方法:update
                          参数:Channel view(实体类)
                          调用Sql：channelService.update
                       删除栏目信息:
                          @RequestMapping("/delete")
                          方法:delete
                          参数:Integer id
                  文章管理:
                       查询全部文章:
                          Controller:PostController
                          @RequestMapping("/list")
                          方法:list
                          参数:String title, ModelMap model, HttpServletRequest request
                          调用Sql：channelService.findAll
                       文章编辑：
                          @RequestMapping(value = "/view", method = RequestMethod.GET)
                          方法:toUpdate
                          参数:Long id, ModelMap model
                          查询文章:channelService.findAll(Consts.IGNORE)
                       更新文章:
                          @RequestMapping(value = "/update", method = RequestMethod.POST)
                          方法:subUpdate
                          参数:PostVO post
                          调用Sql:postService.update
                       删除文章:
                          @RequestMapping("/delete") 
                          方法:delete
                          参数:List<Long> id
                          调用Sql:postService.delete       
                       推荐文章:
                          @RequestMapping("/featured")
                          方法:featured
                          参数:Long id
                          调用Sql:postService.updateFeatured
                       文章置顶:
                          @RequestMapping("/weight")
                          方法:weight
                          参数:Long id
                          调用Sql方法:postService.updateWeight
                       文章推荐:                       
                          @RequestMapping("/featured")
                          对应方法:featured 
                          参数:Long id, HttpServletRequest request
                          Sql语句调用:postService.updateFeatured
                       评论删除:
                                    @RequestMapping("/delete")
                                    方法:delete
                                    参数:List<Long> id
                                    Sql语句调用:commentService.delete(id);
                       查询全部评论:
                                    @RequestMapping("/delete")
                                    方法:delete
                                    参数:List<Long> id
                                    Sql语句调用:commentService.delete(id);       
                       查询评论:
                             @RequestMapping("/list")
                             Sql语句调用:commentService.paging4Admin
                             转发重定向:return "/admin/comment/list";  
                       用户管理:
                                  查询全部账户信息:
                                     Controller:UserController
                                     @RequestMapping("/list")
                                     方法:list
                                     参数:String name, ModelMap model
                                     重定向:return "/admin/user/list";
                                  修改角色:
                                     1.查询:
                                     Controller:UserController
                                     @RequestMapping("/view")
                                     方法:view
                                     参数：Long id, ModelMap model
                                     Sql调用:userRoleService.listRoles
                                     重定向:return "/admin/user/view";
                                     2.更改
                                     @PostMapping("/update_role")
                                     方法:postAuthc
                                     参数:Set<Long> roleIds, ModelMap model
                                     调用Sql语句:userRoleService.updateRole
                                     重定向:return "redirect:/admin/user/list";
                                  账户激活:
                                     @RequestMapping("/open")
                                     方法:open
                                     参数:Long id
                                     Sql语句调用:userService.updateStatus
                                  账户禁用:
                                     @RequestMapping("/close")
                                     方法:close
                                     参数:Long id
                                     Sql语句调用:userService.updateStatus
                                  修改密码:
                                     1.查询:
                                     @RequestMapping(value = "/pwd", method = RequestMethod.GET)
                                     方法:pwsView
                                     参数:Long id, ModelMap model
                                     Sql调用语句:userService.get
                                     转发重定向:return "/admin/user/pwd";
                                     2.修改:
                                     @RequestMapping(value = "/pwd", method = RequestMethod.POST)
                                     方法:pwd
                                     参数:Long id, String newPassword, ModelMap model
                                     调用Sql语句:userService.updatePassword
                                     转发重定向:return "/admin/user/pwd";
                                  角色管理:
                                      1.查询角色信息:
                                      Controller:RoleController
                                      @GetMapping("/list")
                                      方法:paging
                                      参数:String name, ModelMap model
                                      调用Sql:roleService.paging
                                      编辑/修改:
                                      @RequestMapping("/view")
                                      方法:view
                                      参数:Long id, ModelMap model
                                      调用Sql方法:roleService.get
                                      转发重定向:return "/admin/role/view";
                                      2.修改角色信息:
                                      @RequestMapping("/update")
                                      方法:update
                                      参数:Role role,List<Long> perms, ModelMap model
                                      循环数组: 
                                       for(Long pid: perms){
                                       Permission p = new Permission();
                                       p.setId(pid);
                       	            permissions.add(p);
                                        }
                                      然后将数组放进进行更新:
                                      roleService.update(role, permissions(数组));
                                      
                               
                          
                   
                          
                          
                             
                                    