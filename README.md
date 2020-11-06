# tree-tu-y
uniapp 纵轴树状图

# 前言
进入github下载完整包，地址：[github地址](https://github.com/ZhouLiangLiangJS/treeTuY) 
创作不宜，喜欢的给我点个star，坚持更新

# 使用方法

```
//引入number-jpan组件
	import treeTuY from '../../components/treeTuY.vue'
//注册组件
components: {
			treeTuY
		}
```

```
<tree-tu-y :serverData="serverData" @dataChange="change"></tree-tu-y>
------------------------------------------------------------------------
	serverData:       需要渲染的数据，需要传入指定数据结构（请看下文完整代码）
	dataChange:       当数据发生变化时触发第一个参数为新的数据
------------------------------------------------------------------------

```


# 完整代码
# 
```
<template>
	<view class="content">
		<tree-tu-y :serverData="serverData" @dataChange="change"></tree-tu-y>
	</view>
</template>

<script>
	import treeTuY from '../../components/treeTuY.vue'
	export default {
		components: {
			treeTuY
		},
		data() {
			return {
				serverData: {
					title: '报道新生',
					ArrC: [{
							title: '船舶专业群',
							child: [{
								title: '船舶2001班'
							}]
						},
						{
							title: '船舶专业群',
							child: [{
									title: '船舶2001班'
								},{
									title: '船舶2001班'
								}
							]
						}
					]
				}
			}
		},
		onLoad() {

		},
		methods: {
			change(res){
				console.log(res)
			}
		}
	}
</script>


```


