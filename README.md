官方的github地扯为：https://github.com/kindsoft/kindeditor
本包是为了本人在项目中快速Fetch而上传上的
编辑器PHP使用方法

在需要显示编辑器的位置添加textarea输入框。
<textarea id="editor_id" name="content" style="width:700px;height:300px;">
&lt;strong&gt;HTML内容&lt;/strong&gt;
</textarea>

<script charset="utf-8" src="/editor/kindeditor.js"></script>
<script charset="utf-8" src="/editor/lang/zh_CN.js"></script>
<script>
        KindEditor.ready(function(K) {
                window.editor = K.create('#editor_id');
        });
</script>
Note
第一个参数可用其它CSS选择器，匹配多个textarea时只在第一个元素上加载编辑器。
通过K.create函数的第二个参数，可以对编辑器进行配置，具体参数请参考 编辑器初始化参数 。
var options = {
        cssPath : '/css/index.css',
        filterMode : true
};
var editor = K.create('textarea[name="content"]', options);
4. 获取HTML数据

// 取得HTML内容
html = editor.html();

// 同步数据后可以直接取得textarea的value
editor.sync();
html = document.getElementById('editor_id').value; // 原生API
html = K('#editor_id').val(); // KindEditor Node API
html = $('#editor_id').val(); // jQuery

// 设置HTML内容
editor.html('HTML内容');
Note
KindEditor的可视化操作在新创建的iframe上执行，代码模式下的textarea框也是新创建的，所以最后提交前需要执行 sync() 将HTML数据设置到原来的textarea。
KindEditor在默认情况下自动寻找textarea所属的form元素，找到form后onsubmit事件里添加sync函数，所以用form方式提交数据，不需要手动执行sync()函数。
KindEditor默认采用白名单过滤方式，可用 htmlTags 参数定义要保留的标签和属性。当然也可以用 filterMode 参数关闭过滤模式，保留所有标签。
// 关闭过滤模式，保留所有标签
KindEditor.options.filterMode = false;

KindEditor.ready(function(K)) {
        K.create('#editor_id');
}