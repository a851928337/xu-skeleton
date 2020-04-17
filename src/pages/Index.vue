<template>
	<div class="index">
		<div class="container">
			<div class="list">
				<XuSkeleton :show="skeleton" prop="list" keyProp="id">
					<!-- 要填充骨架的用skeleton-fill标记，并且使用fill-X(X代表数字)表示填充的长度(文本使用) -->
					<div class="item" v-for="item in list" :key="item.id">
						<div class="top">
							<i class="avatar skeleton-fill" />
							<span class="title skeleton-fill fill-6">{{ item.title }}</span>
						</div>
						<p class="content skeleton-fill fill-12">{{ item.content }}</p>
					</div>
				</XuSkeleton>
			</div>
		</div>
	</div>
</template>
<script>
import XuSkeleton from '../components/XuSkeleton';
export default {
	name: 'index',
	components: { XuSkeleton },
	data() {
		return {
			list: [],
			skeleton: true
		};
	},
	mounted() {
		setTimeout(() => {
			this.list = [
				{
					id: 1,
					avatar: '',
					title: '我是标题1',
					content: '我是内容1我是内容1我是内容1我是内容1'
				},
				{
					id: 2,
					avatar: '',
					title: '我是标题2',
					content: '我是内容2我是内容2我是内容2我是内容2'
				},
				{
					id: 3,
					avatar: '',
					title: '我是标题3',
					content: '我是内容3我是内容3我是内容3我是内容3'
				},
				{
					id: 4,
					avatar: '',
					title: '我是标题4',
					content: '我是内容4我是内容4我是内容4我是内容4'
				}
			];
			this.skeleton = false;
		}, 5000);
	}
};
</script>
<style lang="less" scoped>
.index {
	.container {
		margin-top: 40px;
		height: 80vh;
		.list {
			display: inline-block;
			height: 100%;
			width: 300px;
			overflow: hidden;
			.item {
				width: 100%;
				box-sizing: border-box;
				height: 90px;
				border-radius: 4px;
				border: 0.5px solid rgba(0, 0, 0, 0.2);
				padding: 10px;
				&:not(:first-child) {
					margin-top: 10px;
				}
				.top {
					text-align: left;
					& > * {
						display: inline-block;
						vertical-align: middle;
					}
					.avatar {
						width: 30px;
						height: 30px;
						border: 1px solid gray;
						border-radius: 50%;
					}
					.title {
						margin-left: 10px;
					}
				}
				.content {
					margin-top: 15px;
					overflow: hidden;
					text-overflow: ellipsis;
					white-space: nowrap;
				}
			}
		}
	}
}
</style>
