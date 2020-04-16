<template>
  <div class="xu-skeleton">
    <div v-if="skeletonShow" ref="template-container" class="template-container">
      <slot name="template"></slot>
    </div>
    <div v-show="!skeletonShow" ref="content-container" class="content-container">
      <slot name="content"></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "xu-skeleton",
  props: {
    prop: {
      required: true
    },
    loop: {
      default: "auto"
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
      if (!this.prop.length) this.skeletonShow = true;
      this.$nextTick(() => {
        if (this.skeletonShow) {
          const slot = this.$refs["template-container"];
          const el = slot.childNodes[0].cloneNode(true);
          const fills = el.querySelectorAll(".skeleton-fill");
          fills.forEach(item => {
            const fill = item.getAttribute("fill");
            if (fill) {
              item.innerHTML = "&emsp;".repeat(Number(fill));
            }
          });
          if (this.loop === "auto") {
            const parentNode = slot.parentNode.parentNode;
            const containerHeight = parentNode.clientHeight;
            const templateHeight = slot.childNodes[0].clientHeight;
            const length = parseInt(containerHeight / templateHeight);
            slot.innerHTML = "";
            for (let i = 0; i < length; i++) {
              slot.appendChild(el.cloneNode(true));
            }
          }
        }
      });
    }
  },
  watch: {
    prop: {
      handler: function(n) {
        if (n.length) this.skeletonShow = false;
      },
      deep: true
    }
  }
};
</script>
<style lang="less" scoped>
.xu-skeleton {
  .template-container {
    .skeleton-fill {
      animation: skeletonBackground 1.2s linear infinite;
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
}
</style>