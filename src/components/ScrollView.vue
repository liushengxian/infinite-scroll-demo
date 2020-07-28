<template>
  <div class="scroll-view" @scroll="handleScroll">
    <ul ref="scrollList">
      <li v-for="(item, index) in computedList" :key="index" class="list-item">
        <h1>Test item {{ item.index }}</h1>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ScrollView',
  data() {
    return {
      arraylist: [],
      loadingFlag: false,
      index: 0,
    };
  },
  computed: {
    computedList() {
      return this.arraylist.slice(-20);
    },
  },
  methods: {
    handleScroll(e) {
      const a = e.target;
      if (this.loadingFlag) {
        return;
      }
      if (a.scrollTop + document.body.scrollHeight >= a.scrollHeight - 10) {
        this.requestNewItem(5);
        a.scrollTop -= a.scrollHeight / 4;
      }
      if (this.arraylist.length <= 20) {
        return;
      }
      if (a.scrollTop === 0) {
        this.requestNewItem(-5);
        a.scrollTop = a.scrollHeight / 4;
      }
    },
    requestNewItem(count) {
      this.loadingFlag = true;
      if (count > 0) {
        for (let i = 0; i < count; i++) {
          this.arraylist.push({
            name: 'test',
            index: this.index + i,
          });
        }
      } else {
        for (let i = 0; i < Math.abs(count); i++) {
          this.arraylist.pop();
        }
      }
      this.index += count;
      setTimeout(() => {
        this.loadingFlag = false;
      }, 500);
    },
  },
  mounted() {
    this.requestNewItem(20);
  },
};
</script>

<style lang="stylus" scoped>
.scroll-view
    width 100%
    height 100vh
    flex 1
    overflow scroll
    box-sizing border-box
    ul
        margin 0
        padding 0
        list-style-type none
    .list-item
        margin 10px
        height 200px
        border 1px solid #eee
</style>
