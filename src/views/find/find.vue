<template>
	
	<div class="find-content">
		<!-- 导航栏开始 -->
		<div class="top">
			<ul>
				<li><a @click="toPage(`/find`),changeClass()" class="current">中奖信息</a></li>
				<li><a @click="toPage(`/find-yesterday`),changeClass()">昨日盈利榜</a></li>
			</ul>
		</div>
		<!-- 导航栏结束 -->
		
		<div class="act-item" v-for="(item,index) in finds" @click="toPage(`/player/${index}`)" v-bind:key="item.id">
			<div class="num">
				<img v-bind:src="item.src">
			</div>
			<div class="text">
				<strong>{{item.top1}}</strong>
				<span>{{item.top2}}<br>{{item.bottom1}}</span><em>{{item.bottom2}}</em>
			</div>
			<div class="act-icon">
				<i class="right-iconfont icon-youjiantou" style="color:#999"></i>
			</div>
		</div>
	</div>
</template>

<script>
	import Navbar from '@/components/Navbar.vue';
	
	export default {
		name: "find",
		components: {
			Navbar
		},
		data(){
			return {
				finds: [
					{
						id: 1,
						src: "./../../../static/images/player1.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 2,
						src: "./../../../static/images/player2.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 3,
						src: "./../../../static/images/player3.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 4,
						src: "./../../../static/images/player4.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 5,
						src: "./../../../static/images/player5.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 6,
						src: "./../../../static/images/player6.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 7,
						src: "./../../../static/images/player7.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 8,
						src: "./../../../static/images/player8.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 9,
						src: "./../../../static/images/player9.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					},
					{
						id: 10,
						src: "./../../../static/images/player10.jpg",
						top1: "151***g",
						top2: "在上海",
						bottom1: "喜中",
						bottom2: "￥2.3"
					}
				]
			}
		},
		methods: {
			toPage(link) {
				this.$router.push(link)
			},
			changeClass(){
				this.class = "change";
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import "../../styles/index";
	@import "./styles/main";
</style>
