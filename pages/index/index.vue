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
