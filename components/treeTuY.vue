<template>
	<view class="main">
		<view class="xiugai">
			<view class="xiugai_btn" :style="flag?'':'background:red'" @click="xiugai()">{{flag?'修改':'保存'}}</view>
		</view>
		<view class="main_cen center">
			<view class="cen_lei">
				<view class="cen_button_A">
					<input style="font-weight: 400;" v-model="data.title" :disabled="flag" />
					<em class="center-x"></em>
				</view>
				<view class="cen_xian" :style="'width:'+(flag?(data.ArrC.length-1):(data.ArrC.length))*200+'px;'"></view>
				<view class="cen_fenban_box" :style="'width:'+(flag?(data.ArrC.length):(data.ArrC.length+1))*200+'px;'">
					<view class="cen_fenban" v-for="(item,i) in data.ArrC" :key="i">
						<input type="text" v-model="item.title" :disabled="flag" />
						<em class="center-x"></em>
						<text class="svg" v-if="!flag"  @click="delChild(data.ArrC,i)">
							<svg t="1604300688569" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
							 p-id="3072" width="20" height="20">
								<path d="M512.175497 775.053138c12.68695 0 22.983457-10.296507 22.983457-22.982434L535.158954 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.983457 10.296507-22.983457 22.982434l0 321.755098C489.193063 764.756631 499.48957 775.053138 512.175497 775.053138z"
								 p-id="3073"></path>
								<path d="M650.071124 775.053138c12.685927 0 22.982434-10.296507 22.982434-22.982434L673.053558 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.982434 10.296507-22.982434 22.982434l0 321.755098C627.08869 764.756631 637.384174 775.053138 650.071124 775.053138z"
								 p-id="3074"></path>
								<path d="M374.280894 775.053138c12.685927 0 22.982434-10.296507 22.982434-22.982434L397.263327 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.982434 10.296507-22.982434 22.982434l0 321.755098C351.29846 764.756631 361.593943 775.053138 374.280894 775.053138z"
								 p-id="3075"></path>
								<path d="M833.930595 154.525376 696.035992 154.525376 696.035992 108.559485c0-25.372877-20.590967-45.964868-45.964868-45.964868L374.280894 62.594617c-25.372877 0-45.965891 20.546965-45.965891 45.964868l0 45.964868L190.420399 154.524352c-25.372877 0-45.964868 20.591991-45.964868 45.964868l0 45.964868c0 25.372877 20.591991 45.964868 45.964868 45.964868l0 574.563918c0 50.745754 41.138956 91.928712 91.930759 91.928712l459.650725 0.002047c50.745754 0 91.929736-41.138956 91.929736-91.930759L833.931618 292.419979c25.372877 0 45.965891-20.545942 45.965891-45.964868l0-45.964868C879.896486 175.117366 859.303472 154.525376 833.930595 154.525376zM374.280894 129.496329c0-12.685927 10.296507-22.982434 22.982434-22.982434l229.825362 0c12.68695 0 22.982434 10.296507 22.982434 22.982434l0 22.982434c-22.246677 0-275.79023 0-275.79023 0L374.280894 129.496329zM787.966751 866.983897c0 25.372877-20.593014 45.963845-45.965891 45.963845L282.351158 912.947741c-25.3739 0-45.965891-20.590967-45.965891-45.963845L236.385267 292.419979c31.578206 0 525.748119 0 551.582507 0L787.967774 866.983897zM810.948161 246.455111 213.402833 246.455111c-12.685927 0-22.982434-10.296507-22.982434-22.981411 0-12.685927 10.296507-22.982434 22.982434-22.982434l597.546352 0c12.685927 0 22.982434 10.296507 22.982434 22.982434C833.930595 236.158604 823.635111 246.455111 810.948161 246.455111z"
								 p-id="3076"></path>
							</svg>
						</text>
					</view>
					<view class="cen_fenban" style="cursor: pointer;" @click="addItem()" v-if="!flag">
						<text>+</text>
						<em class="center-x"></em>
					</view>
				</view>
				<view class="clearfix">
					<view class="cen_fenban_child" v-for="(item,i) in data.ArrC" :key="i">
						<view class="cen_fenban_child_leftX" v-if="!item.child.length==0||!flag" :style="'height:'+(((flag?(item.child.length):(item.child.length+1))*60)-20)+'px;'"></view>
						<view class="cen_fenban_child_box" v-for="(child,n) in item.child" :key="n">
							<input type="text" v-model="child.title" placeholder="请输入内容" :disabled="flag" />
							<em class="center-y"></em>
							<text class="svg" v-if="!flag" @click="delChild(item.child,n)">
								<svg t="1604300688569" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
								 p-id="3072" width="20" height="20">
									<path d="M512.175497 775.053138c12.68695 0 22.983457-10.296507 22.983457-22.982434L535.158954 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.983457 10.296507-22.983457 22.982434l0 321.755098C489.193063 764.756631 499.48957 775.053138 512.175497 775.053138z"
									 p-id="3073"></path>
									<path d="M650.071124 775.053138c12.685927 0 22.982434-10.296507 22.982434-22.982434L673.053558 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.982434 10.296507-22.982434 22.982434l0 321.755098C627.08869 764.756631 637.384174 775.053138 650.071124 775.053138z"
									 p-id="3074"></path>
									<path d="M374.280894 775.053138c12.685927 0 22.982434-10.296507 22.982434-22.982434L397.263327 430.314583c0-12.685927-10.296507-22.982434-22.982434-22.982434s-22.982434 10.296507-22.982434 22.982434l0 321.755098C351.29846 764.756631 361.593943 775.053138 374.280894 775.053138z"
									 p-id="3075"></path>
									<path d="M833.930595 154.525376 696.035992 154.525376 696.035992 108.559485c0-25.372877-20.590967-45.964868-45.964868-45.964868L374.280894 62.594617c-25.372877 0-45.965891 20.546965-45.965891 45.964868l0 45.964868L190.420399 154.524352c-25.372877 0-45.964868 20.591991-45.964868 45.964868l0 45.964868c0 25.372877 20.591991 45.964868 45.964868 45.964868l0 574.563918c0 50.745754 41.138956 91.928712 91.930759 91.928712l459.650725 0.002047c50.745754 0 91.929736-41.138956 91.929736-91.930759L833.931618 292.419979c25.372877 0 45.965891-20.545942 45.965891-45.964868l0-45.964868C879.896486 175.117366 859.303472 154.525376 833.930595 154.525376zM374.280894 129.496329c0-12.685927 10.296507-22.982434 22.982434-22.982434l229.825362 0c12.68695 0 22.982434 10.296507 22.982434 22.982434l0 22.982434c-22.246677 0-275.79023 0-275.79023 0L374.280894 129.496329zM787.966751 866.983897c0 25.372877-20.593014 45.963845-45.965891 45.963845L282.351158 912.947741c-25.3739 0-45.965891-20.590967-45.965891-45.963845L236.385267 292.419979c31.578206 0 525.748119 0 551.582507 0L787.967774 866.983897zM810.948161 246.455111 213.402833 246.455111c-12.685927 0-22.982434-10.296507-22.982434-22.981411 0-12.685927 10.296507-22.982434 22.982434-22.982434l597.546352 0c12.685927 0 22.982434 10.296507 22.982434 22.982434C833.930595 236.158604 823.635111 246.455111 810.948161 246.455111z"
									 p-id="3076"></path>
								</svg>
							</text>
						</view>
						<view style="cursor: pointer;" class="cen_fenban_child_box" @click="addChild(i)" v-if="!flag">
							<text>+</text>
							<em class="center-y"></em>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				flag: true,
				data: {},
				oldData: {}
			}
		},
		props: {
			serverData: {}
		},
		created() {
			this.data = this.$props.serverData
		},
		methods: {
			delChild(n,i){
				console.log(n,i)
				n.splice(i,1)
			},
			xiugai() {
				let content = "";
				let that = this;
				if (this.flag) {
					content = '点击需要修改的地方，即可输入修改';
					this.oldData = JSON.parse(JSON.stringify(that.data));
				} else {
					content = '您确定要保存吗？'
				}
				uni.showModal({
					title: '系统提示',
					content,
					showCancel: !that.flag,
					success(res) {
						if (!that.flag) {
							if (res.confirm) {
								that.$emit('change', that.data)
							} else {
								that.data = { ...that.oldData
								}
							}
						}
						that.flag = !that.flag;
					}
				})
			},
			addItem() {
				this.data.ArrC.push({
					title: '',
					child: [

					]
				})
			},
			addChild(i) {
				this.data.ArrC[i].child.push({
					title: '',
				})
			}
		}
	}
</script>

<style scoped>
	.clearfix:after {
		content: "";
		display: block;
		height: 0;
		clear: both;
		visibility: hidden;
	}

	.clearfix {
		*zoom: 1;
	}

	.main {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		overflow-x: scroll;
	}

	.main_nav {
		width: 100%;
		line-height: 50px;
		transform: translateY(-100%);
		position: absolute;
		color: #707070;
	}

	.main_nav button {
		float: right;
		border-radius: 0px;
		border: 0px;
		box-shadow: 2px 2px 4px #909193;
	}

	.main_cen {
		background-color: #FFFFFF;
	}

	.cen_lei {
		padding: 50px 30px;
	}

	.cen_button_A {
		background-color: #5c6a7c;
		box-shadow: 0 0 5px #5c6a7c;
		padding: 0 20px;
		color: #FFFFFF;
		line-height: 60px;
		position: relative;
		display: inline-block;
		margin-left: 50%;
		transform: translateX(-50%);
		width: 200px;
		text-align: center;
		font-size: 16px;
		font-weight: 900;
	}

	.cen_button_A input {
		height: 60px;
		width: 100%;
	}

	.cen_button_A>em {
		position: absolute;
		width: 1px;
		height: 10px;
		background-color: #b4de8a;
		bottom: 0;
		transform: translate(-50%, 120%);
	}

	.cen_xian {
		height: 1px;
		background-color: #b4de8a;
		width: 10px;
		transform: translateY(12px);
		margin: 0 auto;
	}

	.xiugai {
		width: 100vw;
		line-height: 30px;
		position: absolute;
		top: 20px;
		right: 0;
	}

	.xiugai_btn {
		display: inline-block;
		width: 80px;
		text-align: center;
		float: right;
		border-radius: 30px;
		cursor: pointer;
		background-color: #52BF8A;
		color: #FFFFFF;
	}

	.cen_fenban_box {
		margin-top: 24px;
		height: 40px;
	}

	.cen_fenban {
		width: 160px;
		height: 40px;
		line-height: 40px;
		text-align: center;
		background-color: #52BF8A;
		float: left;
		color: #FFFFFF;
		margin: 0 20px;
		box-shadow: 2px 2px 4px #909193;
		position: relative;
	}


	.cen_fenban>text {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		display: block;
	}

	.cen_fenban_child {
		width: 160px;
		float: left;
		margin: 0 20px;
		padding-bottom: 10px;
	}

	.cen_fenban_child_leftX {
		width: 1px;
		background-color: #aaa;
		margin-left: 20px;
		float: left;
	}

	.cen_fenban_child_box {
		width: 140px;
		height: 40px;
		margin-top: 20px;
		background-color: #FFFFFF;
		color: #707070;
		box-shadow: 2px 2px 6px #909193;
		margin-left: 40px;
		text-align: center;
		position: relative;
		cursor: pointer;
		line-height: 40px;
	}

	.svg {
		position: absolute;
		right: -25px;
		top: 0;
	}

	.cen_fenban_child_box>text>svg {
		width: 20px;
	}

	.cen_fenban_child_box>input,
	.cen_fenban>input {
		width: 100%;
		line-height: 40px;
		height: 40px;
	}

	.cen_fenban_child_box>em {
		position: absolute;
		width: 20px;
		height: 1px;
		background-color: #AAAAAA;
		left: -20px;
		top: 20px;
	}

	.cen_fenban>em {
		position: absolute;
		width: 1px;
		height: 10px;
		background-color: #b4de8a;
		top: 0;
		transform: translate(-50%, -120%);
	}
</style>
