# Ghost 增加评论模块


<p>Ghost作为一个更加纯粹的博客平台，并没有打算为其开发内置的文章评论功能。而是将评论功能托管给第三方，好处也是让用户更有精力集中于网站内容的建设。实现的办法也很简单，只需要向Ghost主题的模板Handlebars(.hbs)插入第三方评论组件的JavaScript代码来为Ghost博客增加评论功能。 </p>
<p><em>国内最常用的多说评论框，支持国内常见的社交网络一键注册登录、盖楼讨论和分享而且对新用户上手简单。而Disqus功能强大、完善的社交网络和多国语言支持并且为其插件启用全球CDN加速。总的来说两个插件各有所长。</em></p>
<p>基于默认主题Casper的安装指南：</p>
<ul>
<li><a href="index.html#comments.hbs">创建一个模板</a></li>
<li><a href="index.html#Duoshuo">安装多说评论系统</a></li>
<li><a href="index.html#Disqus">安装Disqus</a></li>
</ul>
<hr>
<h4 id="comments.hbs">创建一个模板</h4>
<p>为了在需要评论框代码的时候方便引用，我选择事先在主题文件夹<code>content\themes\casper\partials</code>下面创建一个叫做<strong>comments.hbs</strong>的模板文件，也就是评论框的专属模板。</p>
<p>现在我只需要在我的Casper主题下面的post.hbs模板中的</p>
<pre><code>            &lt;/section&gt;

        &lt;/footer&gt;
    &lt;/article&gt;
&lt;/main&gt;
</code></pre>
<p>前面部分添加一句<code>{{&gt; comments}}</code>就可以展示评论框了。</p>
<p>添加后就像这样：</p>
<pre><code>            &lt;/section&gt;
            {{&gt; comments}}
        &lt;/footer&gt;
    &lt;/article&gt;
&lt;/main&gt;
</code></pre>
<p>这样以来的好处就可以在任何主题中轻松移植评论框代码。</p>
<p>开始之前：对评论框Html代码进行简要说明。</p>
<ul>
<li><code>&lt;section class="post-comments"&gt;...&lt;/section&gt;</code>用于展示评论框</li>
<li><code>&lt;script type="text/javascript"&gt;...&lt;/script&gt;</code>评论框公共代码</li>
<li><code>{{slug}}</code> 引用文章短名作为第三方社交平台识别文章的特征标志</li>
<li><code>{{title}}</code> 引用文章标题</li>
<li><code>{{url absolute="true"}}</code> 获取永久链接</li>
</ul>
<hr>
<h4 id="Duoshuo">安装多说评论框</h4>
<p>1.将下面的评论框代码插入<strong>comments.hbs</strong>文件。 <br>
多说评论框：</p>
<pre><code>&lt;section class="post-comments"&gt;
    &lt;div class="ds-thread" data-thread-key="{{slug}}" data-title="{{title}}" data-url="{{url absolute="true"}}"&gt;&lt;/div&gt;
    &lt;!-- 务必插入多说公共JS代码 --&gt;
&lt;/section&gt;
</code></pre>
<p>2.如何获取多说公共JS代码？</p>
<p>登录多说 &gt; 点击“我要安装”&gt; 创建站点 &gt; 获取公共代码（如图）</p>
<p><img src="https://www.binarization.com/content/images/2015/02/duoshuo-javascript.PNG" alt="多说公共JS代码"></p>
<hr>
<h4 id="Disqus">安装Disqus评论框</h4>
<p>1.将下面的评论框代码插入<strong>comments.hbs</strong>文件。 <br>
Disqus评论框评论框：</p>
<pre><code>  &lt;section class="post-comments"&gt;&lt;div id="disqus_thread"&gt;&lt;/div&gt;
      &lt;!-- 务必插入Disqus公共JS代码 --&gt;
  &lt;/section&gt;
</code></pre>
<p>2.获取Disqus的公共JS代码</p>
<p>注册Disqus &gt; 安装平台选则 Universal Code &gt; 直接复制代码</p>
<p>3.添加完毕后，重新启动Ghost博客。</p>
<p>4.Disqus不能成功加载的时候可以在JavaScript中强制使用HTTPS以链接Disqus服务器。具体方法就是在<code>s.src</code>的提供的URL中加入<code>https://</code>。 </p>

