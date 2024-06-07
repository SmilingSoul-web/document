# 2024/4/17

css属性：

1. pointer-events: none; //禁止鼠标选中
2. user-select: none; //禁止拖拽
3. cursor: pointer; //小手

代码块
` //激活选项卡
const setActiveTab = () => {
activeTab.value = route.path //因为el-tab-pane的name是item.path，所以activeTab也是path
}

	watch(() => route.path, () => {
		//激活选项卡
		setActiveTab()
		//监听路由的变化
		addTabs()
	})
	
	//解决刷新数据页面丢失的问题
	const beforeRefresh = () => {
		window.addEventListener("beforeunload", () => { //监听刷新
			// sessionStorage当浏览器关闭时，结束。localStorage，没有期限
			sessionStorage.setItem('tabsView', JSON.stringify(tabsList.value))
		})
		//页面加载时取数据
		let tabSession = sessionStorage.getItem('tabsView')
		if(tabSession) {
			let oldTabs = JSON.parse(tabSession)
			if(oldTabs.length > 0) {
				store.state.tabsList = oldTabs
			}
		}
	}
	//调用函数需要在模板加载之后调用
	onMounted(() => {
		beforeRefresh()
		setActiveTab()
		addTabs()
	})
	const toggleCollapse = function() {
		isCollapse.value = !isCollapse.value
	}`

# 前端滑动验证组件

vue3-puzzle-vcode
# appID:wx6562ff54366bcd2e

项目本地运行：打包路径配置 config
publicPath: process.env.NODE_ENV === 'production' ? './' : '/',
## 解释
这是一个三元条件运算符（ternary operator）表达式，用来根据不同的条件返回两种可能的值。在这个上下文中，它检查环境变量 process.env.NODE_ENV 是否等于字符串 'production'：
如果是（===），则设置 publicPath 为 './'，表示资源相对于当前 HTML 页面的相对路径。
如果不是，则设置 publicPath 为 '/'，表示资源位于服务器的根目录下。
3. process.env.NODE_ENV 的意义
   process.env.NODE_ENV 是一个环境变量，通常用于标识当前的应用程序运行环境。在 Node.js 和 Webpack 中，常见的取值包括 'development'（开发环境）和 'production'（生产环境）。这个变量有助于开发者针对不同的环境配置不同的构建行为、优化策略以及资源路径等。
   综上所述，这段配置的作用如下：
   当应用处于 生产环境（process.env.NODE_ENV === 'production'），设置 publicPath 为 './'。这意味着在部署到生产服务器后，浏览器会假设所有的静态资源与 HTML 文件位于同一目录下，或者具有相同的基路径。这种设置适用于资源文件被部署到与 HTML 文件紧密关联的目录结构中，例如静态资源被打包并放置在与 HTML 相同的服务器路径下。
   当应用处于 非生产环境（通常是开发环境），设置 publicPath 为 '/'。此时，浏览器会从服务器的根路径开始寻找静态资源。这种设置常见于开发过程中，当使用诸如 Webpack Dev Server 之类的工具时，它会为本地开发提供一个虚拟的服务器环境，所有资源都通过特定端口（如 http://localhost:8080/）访问。将 publicPath 设置为 '/' 可确保开发过程中资源请求指向正确的开发服务器地址。
   通过这样的条件判断，该配置确保了在不同环境中，静态资源都能够被正确地定位和加载，从而保证应用的正常运行。实际使用时，需要确保在构建项目时正确设置了 process.env.NODE_ENV 的值，以匹配相应的环境配置。

















``

```js
const circleChartLoad = (i, val, name, status) => {
  var chartDom = document.querySelector(`.circleChart4_${i}`);
  var myChart = echarts.init(chartDom);
  var option;
  option = {
    series: [{
      type: 'gauge', // 仪表盘
      startAngle: 245, // 起始角度
      endAngle: -62, // 结束角度
      max: 3821.42, // 仪表盘最大值
      radius:"81%", //仪表盘的半径
      pointer: { // 仪表盘指针
        show: true, // 是否显示指针
        offsetCenter: ['0%', '-48%'], // 指针偏移
        length: '50%', // 指针长度
        icon: 'https://zkfiles.oss-cn-beijing.aliyuncs.com/zkepC3.0/zhizhen.svg', // 指针图标
        width: 3, //指针的宽度
        itemStyle: { // 指针样式
          borderCap: 'round', // 指针端点
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [ // 指针渐变色
            {
              offset: 0,
              color: '#66FFFF'
            },
            {
              offset: 0.7,
              color: 'rgba(102,255,255,.6)'
            },
            {
              offset: 1,
              color: 'rgba(102,255,255,.1)'
            },
          ]),
        }
      },
      progress: { // 仪表盘进度条
        show: true, // 是否显示进度条
        width: 8,//进度条宽度
        // overlap: false,
        // roundCap: true,
        // clip: false,
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [ // 进度条渐变色
            {
              offset: 0,
              color: '#59F8AC'
            },
            {
              offset: 1,
              color: '#50C0FF'
            },
          ]),
        }
      },
      axisLine: { // 仪表盘轴线
        lineStyle: { // 轴线样式
          width: 20, // 轴线宽度
          // color: '#01071D',
          color: [ // 轴线渐变色
            [0.1, '#2c4c64'], // 0~10% 红轴
            [1, '#2c4c64'], // 10~20% 绿轴
          ],
          opacity: 0.4, // 轴线透明度
        }
      },
      splitLine: { // 仪表盘分隔线
        show: false, // 是否显示分隔线
        distance: 0, // 分隔线距离
        length: 10 // 分隔线长度
      },
      axisTick: { // 仪表盘刻度
        show: false // 是否显示刻度
      },
      axisLabel: { // 仪表盘刻度文字
        show: false, // 是否显示刻度文字
        distance: 50 // 文字距离
      },
      data: [{ // 仪表盘数据
        value: 1643.21,
        // value: 4000.21,
        // value: 47.6,
        name: '实时流量', // 数据名称 仪表盘数据名称
        title: { // 数据名称样式
          offsetCenter: ['0%', '150%'] // 文字位置
        },
        detail: { // 数据值样式
          valueAnimation: true,
          offsetCenter: ['0%', '0'],
          textShadowBlur: 12,
          textShadowColor: '#06B8FB'
        }
      }],
      title: { // 仪表盘标题
        fontSize: 12,
        color: '#fff'
      },
      detail: { // 仪表盘数据值
        fontSize: 13,
        color: '#fff',
        // formatter: '{value}%',
        // formatter: `{value}{a|%}`,
        rich: { // 富文本样式
          a: {
            fontSize: 16,
            color: '#fff',
            verticalAlign: 'bottom',
            width: 20,
            align: 'center',
          }
        }
      },
    }]
  };

  myChart.clear()
  option && myChart.setOption(option);

  myChart.resize({
    animation: {
      duration: 2800,
      easing: 'cubicInOut',
      // delay: 500,
    },
  });
  window.onresize = () => {
    myChart.resize();
  }
}
```





[ecomfe/echarts-for-weixin](https://github.com/ecomfe/echarts-for-weixin)
### 2024/06/07
##### token无感刷新+一次登陆请求

```js
let isRefreshing = false;
let refreshPromise = null;
let refreshSubscribers = [];
let loginPromise = null; // 新增变量，用于存储login请求的Promise

// 登录请求的封装
async function login() {
    if (!loginPromise) {
        loginPromise = new Promise(async (resolve, reject) => {
            try {
                const response = await api2({
                    headers: {
                        "Content-Type": 'application/json'
                    },
                    url: 'api/v5/login',
                    method: 'POST',
                    data: {
                        password: "microbreak12emqx3Qaz!@#job@emqx",
                        username: "admin"
                    }
                });

                localStorage.setItem('Authorization', response.data.token);
                resolve(response.data.token);
            } catch (err) {
                reject(err);
            }
        });
    }
    return loginPromise;
}

function refreshToken() {
    return new Promise((resolve, reject) => {
        if (isRefreshing) {
            // 如果已经在刷新token，则等待token刷新完成
            refreshSubscribers.push(resolve);
        } else {
            isRefreshing = true;
            refreshPromise = new Promise(async (resolvePromise, rejectPromise) => {
                try {
                    const token = await login();
                    isRefreshing = false;
                    // 解决所有等待中的订阅者
                    while (refreshSubscribers.length) {
                        refreshSubscribers.shift()();
                    }
                    resolvePromise(token);
                } catch (err) {
                    isRefreshing = false;
                    while (refreshSubscribers.length) {
                        refreshSubscribers.shift()(err);
                    }
                    rejectPromise(err);
                }
            });
        }

        if (refreshPromise) {
            return refreshPromise.then(token => {
                resolve(token);
            }, err => {
                reject(err);
            });
        } else {
            resolve();
        }
    });
}

// 响应拦截器2
api2.interceptors.response.use(function (response) {
    return response;
}, async function (error) {
    if (error.response.status === 401) {
        try {
            const newToken = await refreshToken();
            // 更新请求头中的token
            error.config.headers.Authorization = `Bearer ${newToken}`;
            // 重试失败的请求
            return api2(error.config);
        } catch (refreshErr) {
            message.error({
                content: 'Token刷新失败，请重新登录',
            });
            // 处理刷新token失败的情况，比如跳转登录页
            return Promise.reject(refreshErr);
        }
    } else {
        message.error({
            content: error.message ? error.message : error.msg,
        });
        return Promise.reject(error);
    }
});
```
