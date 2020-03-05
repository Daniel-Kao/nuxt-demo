<template>
  <div>
    <div class="w3-light-grey">
      <transition
        v-on:before-enter="beforeEnter"
        v-on:enter="enter"
        v-on:after-enter="afterEnter"
        v-on:enter-cancelled="enterCancelled"
        v-on:before-leave="beforeLeave"
        v-on:leave="leave"
        v-on:after-leave="afterLeave"
        v-on:leave-cancelled="leaveCancelled"
      >
        <div
          class="w3-container w3-green w3-center"
          :style="{ width: 0 }"
          v-show="show"
        >
          25%
        </div>
      </transition>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "home",
  data: function() {
    return {
      width: 0,
      show: false
    };
  },
  mounted: async function() {
    const res = await axios.get("http://localhost:3000/progress");
    this.width = Number(res.data.width);
    this.show = true;
  },
  methods: {
    // --------
    // 进入中
    // --------

    beforeEnter: function(el) {
      // ...
    },
    // 当与 CSS 结合使用时
    // 回调函数 done 是可选的
    enter: function(el, done) {
      this.$velocity(el, { width: this.width + "%" }, { duration: 1000 });
      // ...
      done();
    },
    afterEnter: function(el) {
      // ...
    },
    enterCancelled: function(el) {
      // ...
    },

    // --------
    // 离开时
    // --------

    beforeLeave: function(el) {
      // ...
    },
    // 当与 CSS 结合使用时
    // 回调函数 done 是可选的
    leave: function(el, done) {
      // ...
      done();
    },
    afterLeave: function(el) {
      // ...
    },
    // leaveCancelled 只用于 v-show 中
    leaveCancelled: function(el) {
      // ...
    }
  }
};
</script>

<style scoped>
.w3-light-grey {
  height: 20px;
  width: 100%;
  background-color: gray;
}
.w3-green,
.w3-hover-green:hover {
  color: #fff !important;
  background-color: #4caf50 !important;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
