<template>
  <div class="nav-container">
    <nav class="nav" role="navigation" ref="nav">
      <a
        v-for="(item, index) in navItems"
        :key="index"
        class="nav__item"
        :class="{'nav__item--active': selected === index}"
        @click="select($event, index)"
        :href="item.href"
      >{{item.label}}</a>
      <!--:style="magicShapeStyles"-->
      <span class="nav__magic-line"></span>
    </nav>
    <component :is="'style'" type="text/css">
      .nav__item:nth-child(1).nav__item--active ~ .nav__magic-line {
      top:25%;
      }
      .nav__item:nth-child(2).nav__item--active ~ .nav__magic-line {
      top:50%
      }
      .nav__item:nth-child(3).nav__item--active ~ .nav__magic-line {
      top:75%
      }
      .nav__item:nth-child(4).nav__item--active ~ .nav__magic-line {
      top:100%
      }
    </component>
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
      //this.syncMagicShape(ele);
    },
    syncMagicShape(ele) {
      const { offsetLeft, offsetTop, offsetHeight, offsetWidth } = ele;

      this.magicShapeStyles = {
        width: `${offsetWidth}px`,
        height: `${offsetHeight}px`,
        top: `${offsetTop}px`,
        left: `${offsetLeft}px`
      };
    }
  },
  mounted() {
    //this.syncMagicShape(this.$refs.nav.children[0]);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
nav {
  position: relative;
  display: flex;
  flex-direction: row;
  a {
    text-decoration: none;
    color: #42b983;
    font-weight: bold;
    padding: 1rem;
    transition: color 0.3s linear;
    &:hover {
      color: #4d8b6f;
    }
    &.nav__item--active {
      color: rgb(218, 248, 233);
    }
  }
  .nav__magic-line {
    position: absolute;
    top: 25%;
    left: 0;
    width: 20%;
    height: 2px;
    pointer-events: none;
    border: 1px solid #fff;
    border-width: 0 2px;
    background: #1a5a34;
    -webkit-transition: -webkit-transform 0.5s;
    transition: all 0.5s;
    -webkit-transition-timing-function: cubic-bezier(1, 0.01, 0, 1);
    -webkit-transition-timing-function: cubic-bezier(1, 0.01, 0, 1.22);
    transition-timing-function: cubic-bezier(1, 0.01, 0, 1.22);
  }
}
</style>
