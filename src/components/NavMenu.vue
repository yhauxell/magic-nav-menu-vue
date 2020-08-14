<template>
  <div class="nav-container">
    <nav class="nav" role="navigation" ref="nav">
      <a
        v-for="(item, index) in navItems"
        :key="index"
        class="nav-item"
        :class="{active: selected === index}"
        @click="select($event, index)"
        :href="item.href"
      >{{item.label}}</a>
      <span :style="magicShapeStyles" class="magicShape"></span>
    </nav>
  </div>
</template>

<script>
export default {
  name: "NavMenu",
  props: {
    navItems: {
      type: Array,
      default: () => [
        { href: "#home", label: "Home" },
        { href: "#books", label: "Books" },
        { href: "#pricing", label: "Princing" },
        { href: "#contact", label: "Contact us" }
      ]
    }
  },
  data() {
    return {
      selected: 0,
      magicShapeStyles: null
    };
  },
  methods: {
    select($event, index) {
      this.selected = index;
      const ele = $event.target;
      this.syncMagicShape(ele);
    },
    syncMagicShape(ele) {
      const { offsetLeft, offsetTop } = ele;
      const { width, height } = ele.getBoundingClientRect();

      this.magicShapeStyles = {
        width: `${width}px`,
        height: `${height}px`,
        top: `${offsetTop}px`,
        left: `${offsetLeft}px`
      };
    }
  },
  mounted() {
    this.syncMagicShape(this.$refs.nav.children[0]);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
nav {
  position: relative;
  display: flex;
  flex-direction: column;
  a {
    text-decoration: none;
    color: #42b983;
    font-weight: bold;
    padding: 1rem;
    transition: color 0.3s linear;
    &:hover {
      color: #4d8b6f;
    }
    &.active {
      color: rgb(218, 248, 233);
    }
  }
  .magicShape {
    top: 0;
    left: 0;
    display: block;
    position: absolute;
    background: #11ad5f;
    border-radius: 20px;
    min-width: 698px;
    min-height: 22px;
    transition: all 0.3s ease-in-out;
    z-index: -1;
  }
}
</style>
