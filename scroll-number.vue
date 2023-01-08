<template>
  <div style="display: flex;">
    <div v-for="(item, index) in numberList" :key="index" style="display: flex;">
      <span v-if="isNaN(item)">{{ item }}</span>
      <div class="number" v-else>
        <span class="number-item" ref="numberItem" :data-number="item" :data-index="index">0123456789</span>
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  props: {
    value: {
      type: [String, Number],
      default: 0
    }
  },
  watch: {
    value(newVal) {
      if (newVal) {
        this.$nextTick(() => {
          this.setNumberTransform();
        });
      }
    }
  },
  computed: {
    numberList() {
      return String(this.value).split("");
    }
  },
  data() {
    return {};
  },
  methods: {
    // 设置每一位数字的偏移
    setNumberTransform() {
      let numberItems = this.$refs.numberItem;
      Array.from(numberItems).forEach(c => {
        let value = c.dataset.number;
        c.style.transform = `translateY(-${value * 10}%)`;
      });
    }
  },
  mounted() {
    this.setNumberTransform();
  }
};
</script>
  
<style scoped lang="scss">
.number {
  height: 1.35rem;
  overflow: hidden;

  >span {
    writing-mode: vertical-rl;
    text-orientation: upright;
    transform: translateY(0%);
    margin-right: -0.48rem;
    width: 1.28rem;
    transition: transform 1s;
  }
}
</style>