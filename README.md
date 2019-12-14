# goods

这个网上书城系统使用Eclipse开发，数据库采用MySQL5.5，服务器为Tomcat 8.5。
本系统包含九个模块，前台包含：用户模快，分类模块，图书模块，购物车模块，订单模块；
后台包含：管理员模块， 分类管理模快，图书管理模快，订单管理模块。
项目的数据库脚本在webapp/sql/文件夹下。
1.前台：
 1). 用户模块功能有：
   * 用户注册: 
     > 表单页面是jQuery做校验(包含了ajax异步请求)
       # 在输入框失去焦点时进行校验；
       # 在提交时对所有输入框进行校验；
       # 在输入框得到焦点时，隐藏错误信息。
     > 表单页面使用一次性图形验证码；
     > 在servlet中再次做了表单校验。
   * 用户登录：
     > 表单校验与注册功能相同；
     > 登录成功时会把当前用户名保存到cookie中，为了在登录页面的输入框中显示！
   * 用户退出：销毁session
 2). 分类模块
   * 查询所有分类：
     > 有1级和2级分类
     > 在页面中使用手风琴式菜单(Javascript组件)显示分类。
 3). 图书模块：
   * 按分类查询
   * 按作者查询
   * 按出版社查询
   * 按书名模糊查询
   * 多条件组合查询
   * 按id查询
   除按id查询外，其他都是分页查询。
   技术难点：
     > 组合查询：根据多个条件拼凑sql语句。
     > 带条件分页查询：条件可能会丢失。使用自定义的PageBean来传递分页数据！
     > 页面上的分页导航：页码列表的显示不好计算！
 4). 购物车模块：
   * 添加条目
   * 修改条目数量
   * 删除条目
   * 批量删除条目
   * 我的购物车
   * 查询被勾选条目
   购物车没有使用sesson或cookie，而是存储到数据库中。
   技术难点：
     > 添加条目时，如果两次添加针对同一本书的条目，不是添加，而是合并；
     > 修改数量时使用ajax时请求服务器端，服务器端返回json。
     > 大量js代码
 5). 订单模块：
   * 生成订单
   * 我的订单
   * 查看订单详细
   * 订单支付
   * 订单确认收货
   * 取消订单
   技术难点：
     > 使用易宝在线支付平台：
       # 按照易宝支付范围与易宝支付网关对接。
       # 接收易宝的两种应答机制，针对点对点应答给予回复。
       # 处理多次应答照成的数据库重复确认。
2 后台
 1). 管理员
   * 管理员登录
 2). 分类管理
   * 添加1级分类
   * 添加2级分类: 需要为2级分类指定所属1级分类
   * 编辑1级分类
   * 编辑2级分类: 可以修改所属1级分类
   * 删除1级分类: 存在子分类时，不能删除
   * 删除2级分类: 当前2级分类下存在图书时不能删除
   * 查看所有分类
 3). 图书管理
   * 各种查询：与前台相同
   * 添加图书: 
     > 上传图片
     > 页面中使用动态下拉列表显示2级分类，当指定1级分类后，2级分类下拉列表中动态显示该1级分类下所有2级分类名称
   * 修改图书: 与添加图书相似，也使用动态下拉列表
   * 删除图书: 需要删除图书对应图片，再删除图书
 4). 订单管理
   * 各种查询
   * 订单发货
   * 订单取消