<template>
	<div class="xu-skeleton">
		<div v-if="_show" ref="skeleton-container" class="skeleton-container"></div>
		<div :style="style" ref="content-container" class="content-container">
			<slot></slot>
		</div>
	</div>
</template>
<script>
export default {
	name: 'xu-skeleton',
	props: {
		show: [Boolean],
		keyProp: [String],
		type: {
			default: 'list',
			type: String
		},
		prop: [String],
		loop: {
			default: 'auto'
		}
	},
	data() {
		return {
			skeletonShow: false
		};
	},
	mounted() {
		this.init();
	},
	methods: {
		init() {
			const prop = this.$parent[this.prop];
			// 如果填充类型为auto，判断数据是否为空，如果是，插入一条空数据（获取高度用）
			if (this.loop === 'auto' && !prop.length) {
				this._show = true;
				const item = {};
				item[this.keyProp] = 0;
				this.$parent[this.prop].push(item);
			}
			this.$nextTick(() => {
				if (this._show) {
					// 获取模板高度、模板dom
					const templateHeight = this.$refs['content-container'].childNodes[0]
						.clientHeight;
					const template = this.$refs[
						'content-container'
					].childNodes[0].cloneNode(true);
					const containerHeight = this.$parent.$el.clientHeight;
					// 找到模板中需填充骨架的节点
					const fills = template.querySelectorAll('.skeleton-fill');
					// 根据标记的长度，填充对应的空格字符
					fills.forEach((item) => {
						const fill = item.className.match(/fill-\d*/)
							? item.className.match(/fill-\d*/)[0]
							: '';
						if (fill) {
							item.innerHTML = '&emsp;'.repeat(Number(fill.split('-')[1]));
						}
					});
					if (this.loop === 'auto') {
						// 插入骨架
						const length = parseInt(containerHeight / templateHeight);
						for (let i = 0; i < length; i++) {
							this.$refs['skeleton-container'].appendChild(
								template.cloneNode(true)
							);
						}
					}
				}
			});
		}
	},
	computed: {
		style() {
			return {
				visibility: this._show ? 'hidden' : 'visible'
			};
		},
		_show: {
			get() {
				return this.show;
			},
			set(val) {
				this.$emit('show:update', val);
			}
		}
	}
};
</script>
<style lang="less" scoped>
.xu-skeleton {
	.skeleton-container {
		.skeleton-fill {
			animation: skeletonBackground 1.2s linear infinite;
		}
	}
}
@keyframes skeletonBackground {
	0% {
		// background: linear-gradient(90deg,#e9e9e9);
		background: #d2d2d2;
	}
	50% {
		background: #e9e9e9;
	}
	100% {
		background: #d2d2d2;
	}
}
</style>
