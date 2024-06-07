<template><div><h1 id="_2024-4-17" tabindex="-1"><a class="header-anchor" href="#_2024-4-17" aria-hidden="true">#</a> 2024/4/17</h1>
<p>css属性：</p>
<ol>
<li>pointer-events: none; //禁止鼠标选中</li>
<li>user-select: none; //禁止拖拽</li>
<li>cursor: pointer; //小手</li>
</ol>
<p>代码块
` //激活选项卡
const setActiveTab = () =&gt; {
activeTab.value = route.path //因为el-tab-pane的name是item.path，所以activeTab也是path
}</p>
<pre><code>watch(() =&gt; route.path, () =&gt; {
	//激活选项卡
	setActiveTab()
	//监听路由的变化
	addTabs()
})

//解决刷新数据页面丢失的问题
const beforeRefresh = () =&gt; {
	window.addEventListener(&quot;beforeunload&quot;, () =&gt; { //监听刷新
		// sessionStorage当浏览器关闭时，结束。localStorage，没有期限
		sessionStorage.setItem('tabsView', JSON.stringify(tabsList.value))
	})
	//页面加载时取数据
	let tabSession = sessionStorage.getItem('tabsView')
	if(tabSession) {
		let oldTabs = JSON.parse(tabSession)
		if(oldTabs.length &gt; 0) {
			store.state.tabsList = oldTabs
		}
	}
}
//调用函数需要在模板加载之后调用
onMounted(() =&gt; {
	beforeRefresh()
	setActiveTab()
	addTabs()
})
const toggleCollapse = function() {
	isCollapse.value = !isCollapse.value
}`
</code></pre>
<h1 id="前端滑动验证组件" tabindex="-1"><a class="header-anchor" href="#前端滑动验证组件" aria-hidden="true">#</a> 前端滑动验证组件</h1>
<p>vue3-puzzle-vcode</p>
<h1 id="appid-wx6562ff54366bcd2e" tabindex="-1"><a class="header-anchor" href="#appid-wx6562ff54366bcd2e" aria-hidden="true">#</a> appID:wx6562ff54366bcd2e</h1>
<p>项目本地运行：打包路径配置 config
publicPath: process.env.NODE_ENV === 'production' ? './' : '/',</p>
<h2 id="解释" tabindex="-1"><a class="header-anchor" href="#解释" aria-hidden="true">#</a> 解释</h2>
<p>这是一个三元条件运算符（ternary operator）表达式，用来根据不同的条件返回两种可能的值。在这个上下文中，它检查环境变量 process.env.NODE_ENV 是否等于字符串 'production'：
如果是（===），则设置 publicPath 为 './'，表示资源相对于当前 HTML 页面的相对路径。
如果不是，则设置 publicPath 为 '/'，表示资源位于服务器的根目录下。
3. process.env.NODE_ENV 的意义
process.env.NODE_ENV 是一个环境变量，通常用于标识当前的应用程序运行环境。在 Node.js 和 Webpack 中，常见的取值包括 'development'（开发环境）和 'production'（生产环境）。这个变量有助于开发者针对不同的环境配置不同的构建行为、优化策略以及资源路径等。
综上所述，这段配置的作用如下：
当应用处于 生产环境（process.env.NODE_ENV === 'production'），设置 publicPath 为 './'。这意味着在部署到生产服务器后，浏览器会假设所有的静态资源与 HTML 文件位于同一目录下，或者具有相同的基路径。这种设置适用于资源文件被部署到与 HTML 文件紧密关联的目录结构中，例如静态资源被打包并放置在与 HTML 相同的服务器路径下。
当应用处于 非生产环境（通常是开发环境），设置 publicPath 为 '/'。此时，浏览器会从服务器的根路径开始寻找静态资源。这种设置常见于开发过程中，当使用诸如 Webpack Dev Server 之类的工具时，它会为本地开发提供一个虚拟的服务器环境，所有资源都通过特定端口（如 http://localhost:8080/）访问。将 publicPath 设置为 '/' 可确保开发过程中资源请求指向正确的开发服务器地址。
通过这样的条件判断，该配置确保了在不同环境中，静态资源都能够被正确地定位和加载，从而保证应用的正常运行。实际使用时，需要确保在构建项目时正确设置了 process.env.NODE_ENV 的值，以匹配相应的环境配置。</p>
<p>``</p>
<div class="language-javascript line-numbers-mode" data-ext="js"><pre v-pre class="language-javascript"><code><span class="token keyword">const</span> <span class="token function-variable function">circleChartLoad</span> <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token parameter">i<span class="token punctuation">,</span> val<span class="token punctuation">,</span> name<span class="token punctuation">,</span> status</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">var</span> chartDom <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">querySelector</span><span class="token punctuation">(</span><span class="token template-string"><span class="token template-punctuation string">`</span><span class="token string">.circleChart4_</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>i<span class="token interpolation-punctuation punctuation">}</span></span><span class="token template-punctuation string">`</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">var</span> myChart <span class="token operator">=</span> echarts<span class="token punctuation">.</span><span class="token function">init</span><span class="token punctuation">(</span>chartDom<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">var</span> option<span class="token punctuation">;</span>
  option <span class="token operator">=</span> <span class="token punctuation">{</span>
    <span class="token literal-property property">series</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token punctuation">{</span>
      <span class="token literal-property property">type</span><span class="token operator">:</span> <span class="token string">'gauge'</span><span class="token punctuation">,</span> <span class="token comment">// 仪表盘</span>
      <span class="token literal-property property">startAngle</span><span class="token operator">:</span> <span class="token number">245</span><span class="token punctuation">,</span> <span class="token comment">// 起始角度</span>
      <span class="token literal-property property">endAngle</span><span class="token operator">:</span> <span class="token operator">-</span><span class="token number">62</span><span class="token punctuation">,</span> <span class="token comment">// 结束角度</span>
      <span class="token literal-property property">max</span><span class="token operator">:</span> <span class="token number">3821.42</span><span class="token punctuation">,</span> <span class="token comment">// 仪表盘最大值</span>
      <span class="token literal-property property">radius</span><span class="token operator">:</span><span class="token string">"81%"</span><span class="token punctuation">,</span> <span class="token comment">//仪表盘的半径</span>
      <span class="token literal-property property">pointer</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘指针</span>
        <span class="token literal-property property">show</span><span class="token operator">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> <span class="token comment">// 是否显示指针</span>
        <span class="token literal-property property">offsetCenter</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">'0%'</span><span class="token punctuation">,</span> <span class="token string">'-48%'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token comment">// 指针偏移</span>
        <span class="token literal-property property">length</span><span class="token operator">:</span> <span class="token string">'50%'</span><span class="token punctuation">,</span> <span class="token comment">// 指针长度</span>
        <span class="token literal-property property">icon</span><span class="token operator">:</span> <span class="token string">'https://zkfiles.oss-cn-beijing.aliyuncs.com/zkepC3.0/zhizhen.svg'</span><span class="token punctuation">,</span> <span class="token comment">// 指针图标</span>
        <span class="token literal-property property">width</span><span class="token operator">:</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token comment">//指针的宽度</span>
        <span class="token literal-property property">itemStyle</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 指针样式</span>
          <span class="token literal-property property">borderCap</span><span class="token operator">:</span> <span class="token string">'round'</span><span class="token punctuation">,</span> <span class="token comment">// 指针端点</span>
          <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token keyword">new</span> <span class="token class-name">echarts<span class="token punctuation">.</span>graphic<span class="token punctuation">.</span>LinearGradient</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token punctuation">[</span> <span class="token comment">// 指针渐变色</span>
            <span class="token punctuation">{</span>
              <span class="token literal-property property">offset</span><span class="token operator">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
              <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#66FFFF'</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
              <span class="token literal-property property">offset</span><span class="token operator">:</span> <span class="token number">0.7</span><span class="token punctuation">,</span>
              <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'rgba(102,255,255,.6)'</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
              <span class="token literal-property property">offset</span><span class="token operator">:</span> <span class="token number">1</span><span class="token punctuation">,</span>
              <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'rgba(102,255,255,.1)'</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
          <span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">progress</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘进度条</span>
        <span class="token literal-property property">show</span><span class="token operator">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> <span class="token comment">// 是否显示进度条</span>
        <span class="token literal-property property">width</span><span class="token operator">:</span> <span class="token number">8</span><span class="token punctuation">,</span><span class="token comment">//进度条宽度</span>
        <span class="token comment">// overlap: false,</span>
        <span class="token comment">// roundCap: true,</span>
        <span class="token comment">// clip: false,</span>
        <span class="token literal-property property">itemStyle</span><span class="token operator">:</span> <span class="token punctuation">{</span>
          <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token keyword">new</span> <span class="token class-name">echarts<span class="token punctuation">.</span>graphic<span class="token punctuation">.</span>LinearGradient</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token punctuation">[</span> <span class="token comment">// 进度条渐变色</span>
            <span class="token punctuation">{</span>
              <span class="token literal-property property">offset</span><span class="token operator">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
              <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#59F8AC'</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
              <span class="token literal-property property">offset</span><span class="token operator">:</span> <span class="token number">1</span><span class="token punctuation">,</span>
              <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#50C0FF'</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
          <span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">axisLine</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘轴线</span>
        <span class="token literal-property property">lineStyle</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 轴线样式</span>
          <span class="token literal-property property">width</span><span class="token operator">:</span> <span class="token number">20</span><span class="token punctuation">,</span> <span class="token comment">// 轴线宽度</span>
          <span class="token comment">// color: '#01071D',</span>
          <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token punctuation">[</span> <span class="token comment">// 轴线渐变色</span>
            <span class="token punctuation">[</span><span class="token number">0.1</span><span class="token punctuation">,</span> <span class="token string">'#2c4c64'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token comment">// 0~10% 红轴</span>
            <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token string">'#2c4c64'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token comment">// 10~20% 绿轴</span>
          <span class="token punctuation">]</span><span class="token punctuation">,</span>
          <span class="token literal-property property">opacity</span><span class="token operator">:</span> <span class="token number">0.4</span><span class="token punctuation">,</span> <span class="token comment">// 轴线透明度</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">splitLine</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘分隔线</span>
        <span class="token literal-property property">show</span><span class="token operator">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span> <span class="token comment">// 是否显示分隔线</span>
        <span class="token literal-property property">distance</span><span class="token operator">:</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token comment">// 分隔线距离</span>
        <span class="token literal-property property">length</span><span class="token operator">:</span> <span class="token number">10</span> <span class="token comment">// 分隔线长度</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">axisTick</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘刻度</span>
        <span class="token literal-property property">show</span><span class="token operator">:</span> <span class="token boolean">false</span> <span class="token comment">// 是否显示刻度</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">axisLabel</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘刻度文字</span>
        <span class="token literal-property property">show</span><span class="token operator">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span> <span class="token comment">// 是否显示刻度文字</span>
        <span class="token literal-property property">distance</span><span class="token operator">:</span> <span class="token number">50</span> <span class="token comment">// 文字距离</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">data</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token punctuation">{</span> <span class="token comment">// 仪表盘数据</span>
        <span class="token literal-property property">value</span><span class="token operator">:</span> <span class="token number">1643.21</span><span class="token punctuation">,</span>
        <span class="token comment">// value: 4000.21,</span>
        <span class="token comment">// value: 47.6,</span>
        <span class="token literal-property property">name</span><span class="token operator">:</span> <span class="token string">'实时流量'</span><span class="token punctuation">,</span> <span class="token comment">// 数据名称 仪表盘数据名称</span>
        <span class="token literal-property property">title</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 数据名称样式</span>
          <span class="token literal-property property">offsetCenter</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">'0%'</span><span class="token punctuation">,</span> <span class="token string">'150%'</span><span class="token punctuation">]</span> <span class="token comment">// 文字位置</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token literal-property property">detail</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 数据值样式</span>
          <span class="token literal-property property">valueAnimation</span><span class="token operator">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
          <span class="token literal-property property">offsetCenter</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">'0%'</span><span class="token punctuation">,</span> <span class="token string">'0'</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
          <span class="token literal-property property">textShadowBlur</span><span class="token operator">:</span> <span class="token number">12</span><span class="token punctuation">,</span>
          <span class="token literal-property property">textShadowColor</span><span class="token operator">:</span> <span class="token string">'#06B8FB'</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
      <span class="token literal-property property">title</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘标题</span>
        <span class="token literal-property property">fontSize</span><span class="token operator">:</span> <span class="token number">12</span><span class="token punctuation">,</span>
        <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#fff'</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token literal-property property">detail</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 仪表盘数据值</span>
        <span class="token literal-property property">fontSize</span><span class="token operator">:</span> <span class="token number">13</span><span class="token punctuation">,</span>
        <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#fff'</span><span class="token punctuation">,</span>
        <span class="token comment">// formatter: '{value}%',</span>
        <span class="token comment">// formatter: `{value}{a|%}`,</span>
        <span class="token literal-property property">rich</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token comment">// 富文本样式</span>
          <span class="token literal-property property">a</span><span class="token operator">:</span> <span class="token punctuation">{</span>
            <span class="token literal-property property">fontSize</span><span class="token operator">:</span> <span class="token number">16</span><span class="token punctuation">,</span>
            <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token string">'#fff'</span><span class="token punctuation">,</span>
            <span class="token literal-property property">verticalAlign</span><span class="token operator">:</span> <span class="token string">'bottom'</span><span class="token punctuation">,</span>
            <span class="token literal-property property">width</span><span class="token operator">:</span> <span class="token number">20</span><span class="token punctuation">,</span>
            <span class="token literal-property property">align</span><span class="token operator">:</span> <span class="token string">'center'</span><span class="token punctuation">,</span>
          <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">}</span><span class="token punctuation">]</span>
  <span class="token punctuation">}</span><span class="token punctuation">;</span>

  myChart<span class="token punctuation">.</span><span class="token function">clear</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  option <span class="token operator">&amp;&amp;</span> myChart<span class="token punctuation">.</span><span class="token function">setOption</span><span class="token punctuation">(</span>option<span class="token punctuation">)</span><span class="token punctuation">;</span>

  myChart<span class="token punctuation">.</span><span class="token function">resize</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
    <span class="token literal-property property">animation</span><span class="token operator">:</span> <span class="token punctuation">{</span>
      <span class="token literal-property property">duration</span><span class="token operator">:</span> <span class="token number">2800</span><span class="token punctuation">,</span>
      <span class="token literal-property property">easing</span><span class="token operator">:</span> <span class="token string">'cubicInOut'</span><span class="token punctuation">,</span>
      <span class="token comment">// delay: 500,</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  window<span class="token punctuation">.</span><span class="token function-variable function">onresize</span> <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
    myChart<span class="token punctuation">.</span><span class="token function">resize</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre><div class="line-numbers" aria-hidden="true"><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div></div></div><p><a href="https://github.com/ecomfe/echarts-for-weixin" target="_blank" rel="noopener noreferrer">ecomfe/echarts-for-weixin<ExternalLinkIcon/></a></p>
<h3 id="_2024-06-07" tabindex="-1"><a class="header-anchor" href="#_2024-06-07" aria-hidden="true">#</a> 2024/06/07</h3>
<h5 id="token无感刷新-一次登陆请求" tabindex="-1"><a class="header-anchor" href="#token无感刷新-一次登陆请求" aria-hidden="true">#</a> token无感刷新+一次登陆请求</h5>
<div class="language-javascript line-numbers-mode" data-ext="js"><pre v-pre class="language-javascript"><code><span class="token keyword">let</span> isRefreshing <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
<span class="token keyword">let</span> refreshPromise <span class="token operator">=</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
<span class="token keyword">let</span> refreshSubscribers <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">let</span> loginPromise <span class="token operator">=</span> <span class="token keyword">null</span><span class="token punctuation">;</span> <span class="token comment">// 新增变量，用于存储login请求的Promise</span>

<span class="token comment">// 登录请求的封装</span>
<span class="token keyword">async</span> <span class="token keyword">function</span> <span class="token function">login</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>loginPromise<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        loginPromise <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Promise</span><span class="token punctuation">(</span><span class="token keyword">async</span> <span class="token punctuation">(</span><span class="token parameter">resolve<span class="token punctuation">,</span> reject</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
            <span class="token keyword">try</span> <span class="token punctuation">{</span>
                <span class="token keyword">const</span> response <span class="token operator">=</span> <span class="token keyword">await</span> <span class="token function">api2</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
                    <span class="token literal-property property">headers</span><span class="token operator">:</span> <span class="token punctuation">{</span>
                        <span class="token string-property property">"Content-Type"</span><span class="token operator">:</span> <span class="token string">'application/json'</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token literal-property property">url</span><span class="token operator">:</span> <span class="token string">'api/v5/login'</span><span class="token punctuation">,</span>
                    <span class="token literal-property property">method</span><span class="token operator">:</span> <span class="token string">'POST'</span><span class="token punctuation">,</span>
                    <span class="token literal-property property">data</span><span class="token operator">:</span> <span class="token punctuation">{</span>
                        <span class="token literal-property property">password</span><span class="token operator">:</span> <span class="token string">"microbreak12emqx3Qaz!@#job@emqx"</span><span class="token punctuation">,</span>
                        <span class="token literal-property property">username</span><span class="token operator">:</span> <span class="token string">"admin"</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

                localStorage<span class="token punctuation">.</span><span class="token function">setItem</span><span class="token punctuation">(</span><span class="token string">'Authorization'</span><span class="token punctuation">,</span> response<span class="token punctuation">.</span>data<span class="token punctuation">.</span>token<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token function">resolve</span><span class="token punctuation">(</span>response<span class="token punctuation">.</span>data<span class="token punctuation">.</span>token<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span>err<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token function">reject</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> loginPromise<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">function</span> <span class="token function">refreshToken</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">Promise</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token parameter">resolve<span class="token punctuation">,</span> reject</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>isRefreshing<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// 如果已经在刷新token，则等待token刷新完成</span>
            refreshSubscribers<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>resolve<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            isRefreshing <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
            refreshPromise <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Promise</span><span class="token punctuation">(</span><span class="token keyword">async</span> <span class="token punctuation">(</span><span class="token parameter">resolvePromise<span class="token punctuation">,</span> rejectPromise</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
                <span class="token keyword">try</span> <span class="token punctuation">{</span>
                    <span class="token keyword">const</span> token <span class="token operator">=</span> <span class="token keyword">await</span> <span class="token function">login</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                    isRefreshing <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
                    <span class="token comment">// 解决所有等待中的订阅者</span>
                    <span class="token keyword">while</span> <span class="token punctuation">(</span>refreshSubscribers<span class="token punctuation">.</span>length<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                        refreshSubscribers<span class="token punctuation">.</span><span class="token function">shift</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                    <span class="token punctuation">}</span>
                    <span class="token function">resolvePromise</span><span class="token punctuation">(</span>token<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span>err<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                    isRefreshing <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
                    <span class="token keyword">while</span> <span class="token punctuation">(</span>refreshSubscribers<span class="token punctuation">.</span>length<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                        refreshSubscribers<span class="token punctuation">.</span><span class="token function">shift</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">;</span>
                    <span class="token punctuation">}</span>
                    <span class="token function">rejectPromise</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token keyword">if</span> <span class="token punctuation">(</span>refreshPromise<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> refreshPromise<span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token parameter">token</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
                <span class="token function">resolve</span><span class="token punctuation">(</span>token<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token parameter">err</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
                <span class="token function">reject</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token function">resolve</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// 响应拦截器2</span>
api2<span class="token punctuation">.</span>interceptors<span class="token punctuation">.</span>response<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">response</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> response<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token keyword">async</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">error</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>error<span class="token punctuation">.</span>response<span class="token punctuation">.</span>status <span class="token operator">===</span> <span class="token number">401</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">try</span> <span class="token punctuation">{</span>
            <span class="token keyword">const</span> newToken <span class="token operator">=</span> <span class="token keyword">await</span> <span class="token function">refreshToken</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token comment">// 更新请求头中的token</span>
            error<span class="token punctuation">.</span>config<span class="token punctuation">.</span>headers<span class="token punctuation">.</span>Authorization <span class="token operator">=</span> <span class="token template-string"><span class="token template-punctuation string">`</span><span class="token string">Bearer </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>newToken<span class="token interpolation-punctuation punctuation">}</span></span><span class="token template-punctuation string">`</span></span><span class="token punctuation">;</span>
            <span class="token comment">// 重试失败的请求</span>
            <span class="token keyword">return</span> <span class="token function">api2</span><span class="token punctuation">(</span>error<span class="token punctuation">.</span>config<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span>refreshErr<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            message<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
                <span class="token literal-property property">content</span><span class="token operator">:</span> <span class="token string">'Token刷新失败，请重新登录'</span><span class="token punctuation">,</span>
            <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token comment">// 处理刷新token失败的情况，比如跳转登录页</span>
            <span class="token keyword">return</span> Promise<span class="token punctuation">.</span><span class="token function">reject</span><span class="token punctuation">(</span>refreshErr<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
        message<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
            <span class="token literal-property property">content</span><span class="token operator">:</span> error<span class="token punctuation">.</span>message <span class="token operator">?</span> error<span class="token punctuation">.</span>message <span class="token operator">:</span> error<span class="token punctuation">.</span>msg<span class="token punctuation">,</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> Promise<span class="token punctuation">.</span><span class="token function">reject</span><span class="token punctuation">(</span>error<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre><div class="line-numbers" aria-hidden="true"><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div></div></div></div></template>


