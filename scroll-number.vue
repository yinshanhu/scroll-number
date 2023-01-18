<template>
  <div style="display: flex;">
    <div v-for="(item, index) in numberList" :key="index" style="display: flex;">
      <span v-if="isNaN(item)">{{ item }}</span>
      <div class="number" v-else>
        <div class="number-item" ref="numberItem" :data-number="item" :data-index="index">
          <p>0</p>
          <p>1</p>
          <p>2</p>
          <p>3</p>
          <p>4</p>
          <p>5</p>
          <p>6</p>
          <p>7</p>
          <p>8</p>
          <p>9</p>
        </div>
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
  line-height: 1.35rem;
  height: 1.35rem;
  overflow: hidden;

  .number-item{
    display: flex;
    font-size: 1.41rem;
    color: #D4343B;
    flex-direction: column;
    transform: translateY(0%);
    transition: transform 1s;
  }
}
</style>