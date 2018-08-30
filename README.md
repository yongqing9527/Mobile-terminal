# input-type-input type="search" 实现搜索框
* html5 增加的type=search可以做到（但需要input type=search外面包上一层带action属性的form。

      <div class="search-input-wrap clearfix">
        <div class="form-input-wrap f-l">
            <form action="" class="input-kw-form">
                <input type="search" autocomplete="off" name="baike-search" placeholder="请输入关键词" class="input-kw">
            </form>
            <i class="iconfont if-message"></i>
            <i class="iconfont if-close"></i>
        </div>
        <i class="search-cancel f-l">取消</i>
       </div>
但type=search会有许多默认样式和行为，这次开发遇到的有：
* 会默认下拉框显示搜索历史记录;

* 输入时自动弹出“x”，“x”的样式在不同手机上，样式不同；

* IOS 手机（测试时为iphone6 ios10）上输入框为椭圆形.
但我们希望样式按照我们自定义的样式显示，并且各个手机上能统一。

于是几经google，得到答案：

* 设置input autocomplete="off"去掉弹出的下拉框；

* 将默认的“x”隐藏掉：

      input[type="search"]::-webkit-search-cancel-button{
        display: none;
      }
* 针对ios 设置样式, 去除ios下input 椭圆形:

      -webkit-appearance: none;
      
同时别忘记，如果提交搜索时想使用ajax，那么可以阻止表单的默认行为：

    container.on('submit', '.input-kw-form', function(event){
      event.preventDefault();
    })
