<template>
  <div class="base">
    <div @click="t">asd</div>
    <div v-for="(widget, key) in visibleWidgets" v-bind:key="key">
      <keep-alive>
        <component
          v-bind="{ move: move }"
          v-bind:is="widget.component"
          @click="clickWidget(widget)"
        />
      </keep-alive>
      <keep-alive>
        <widget-box
          v-show="true"
          :widget="widget.component"
          @removeClick="removeClick(widget)"
          visible="true"
        ></widget-box
      ></keep-alive>
    </div>
  </div>
</template>

<script>
import FortniteStats from "./FortniteStats.vue";
import widgetUI from "./WidgetUI.vue";
import widgetBox from "./widgetBox.vue";
export default {
  name: "HelloWorld",
  components: {
    "widget-box": widgetBox,
    "widget-ui": widgetUI,
    FortniteStats: FortniteStats,
  },
  computed: {
    visibleWidgets() {
      return this.$store.getters.visibleWidgets;
    },
    manipulator() {
        return this.$store.manipulator
    }
  },
  props: {
    _style: String,
    msg: String,
  },
  data() {
    return {
      selectedWidget: null,
      visible: [],
    };
  },
  methods: {
    move() {
      widgetBox.updatePosition();
    },
    clickWidget(widget) {
      this.selectedWidget = widget;
    },
    getList() {
      return this.components;
    },
    removeClick(widget) {
      this.manipulator.disableWidget(widget);
    },
    t() {
     this. manipulator.enableW(FortniteStats);
     this. manipulator.getVisible((visible) => {
        this.visible = visible;
      });
    },
  },
  mounted() {},
  update() {
    widgetBox.updatePosition();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.selectedWidget {
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
