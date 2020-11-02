# number-jpan
uniapp 数字键盘

# 前言
进入github下载完整包，地址：[github地址](https://github.com/ZhouLiangLiangJS/number-jpan) 
创作不宜，喜欢的给我点个star，坚持更新

# 使用方法

```
//引入number-jpan组件
import numberJpan from "@/components/numberJpan/numberJpan.vue";
//注册组件
components:{
			'number-jpan':numberJpan
		}
```

```
<number-jpan :length="6" @closeChange="closeChange($event)" :showNum="false" ref="numberPad"></number-jpan>
length:        需要输入多少个字（数字类型）
showNum:       是否显示隐藏输入信息
closeChange：  回调函数通过closeChange的第一个参数可获取值


//初次进入页面触发加载，请将打开加载动画钩子，放入页面
onReady中，放入onLoad中会报错
原因为this.$refs.numberJpan需要找到dom节点，在onLoad时
dom不能保证渲染完毕，在onReady中可在dom渲染完毕才会触发

//打开加载动画
this.$refs.numberJpan.open()

//关闭加载动画
this.$refs.numberJpan.close()

```


# 完整代码
# 
```
<template>
	<view class="content">
		<button type="default" @tap="open()">弹出吧小宝贝</button>
		<view class="">
			{{text}}
		</view>
		<number-jpan :length="6" @closeChange="closeChange($event)" ref="numberPad"></number-jpan>
	</view>
</template>

<script>
	import numberJpan from "@/components/numberJpan/numberJpan.vue";
	export default {
		components:{
			'number-jpan':numberJpan
		},
		data() {
			return {
				text:''
			}
		},
		onLoad() {

		},
		methods: {
			open(){
				this.$refs.numberPad.open()//打开数字输入框
				//this.$refs.numberPad.close()//关闭数字输入框
			},
			closeChange(res){
				console.log(res)
				this.text=res
			}
		}
	}
</script>

```


