---
title: form表单回车提交问题
date: 2017-09-11
categories: html
tags: [html]
---

## form表单回车提交问题,JS监听回车事件

我们有时候希望回车键敲在文本框（input element）里来提交表单（form），但有时候又不希望如此。比如搜索行为，希望输入完关键词之后直接按回车键立即提交表单，而有些复杂表单，可能要避免回车键误操作在未完成表单填写的时候就触发了表单提交。 
要控制这些行为，不需要借助JS，浏览器已经帮我们做了这些处理，这里总结几条规则： 
- 如果表单里有一个type=”submit”的按钮，回车键生效。 
- 如果表单里只有一个type=”text”的input，不管按钮是什么type，回车键生效。 
- 如果按钮不是用input，而是用button，并且没有加type，IE下默认为type=button，FX默认为type=submit。 
- 其他表单元素如textarea、select不影响，radio checkbox不影响触发规则，但本身在FX下会响应回车键，在IE下不响应。 
- type=”image”的input，效果等同于type=”submit”，不知道为什么会设计这样一种type，不推荐使用，应该用CSS添加背景图合适些。 
- 我们在处理表单的页面可以检验他是否点击了按钮来控制下面的程序。if($_POST['submit']){ 如果点击了按钮 程序继续} 
  实际应用的时候，要让表单响应回车键很容易，保证表单里有个type=”submit”的按钮就行。而当只有一个文本框又不希望响应回车键怎么办 呢？我的方法有点别扭，就是再写一个无意义的文本框，隐藏起来。根据第3条规则，我们在用button的时候，尽量显式声明type以使浏览器表现一致。 

通过以上可知只要把type="submit"改成type="button"然后js提交， 在不要有一个type=”text”的input就行了。就不会发生回车跳转。 

但实验发现，ie和火狐不一样，火狐的submit按钮有掩藏的（display：block）和显现的都不行，必须全改，但ie只要显现的没有submit就行了。



 ```js
<script type="text/javascript">   
    document.onkeydown=keyDownSearch; 
    function keyDownSearch(e) {  
        // 兼容FF和IE和Opera  
        var theEvent = e || window.event;  
        var code = theEvent.keyCode || theEvent.which || theEvent.charCode;  
        if (code == 13) {   
            DoSomeThing();//具体处理函数  
            return false;  
        }  
        return true;  
    } 
</script>
 ```

如果只是针对某个DIV层应用回车查询的话，可以将： 
`document.onkeydown=keyDownSearch; `
改成： 
`document.getElementById('层ID').onkeydown=keyDownSearch; `

http://www.cnblogs.com/suizhikuo/p/4925086.html