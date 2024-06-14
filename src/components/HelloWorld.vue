<template>
  <!-- <div class="box" @contextmenu="onContextMenu"></div> -->
  <context-menu v-model:show="show" :options="optionsComponent">
    <context-menu-item
      label="Test item dynamic show and hide"
      :clickClose="false"
      @click="showItem = !showItem"
    />
    <context-menu-item
      v-if="showItem"
      label="Click the item above to show/hide me"
    />
    <context-menu-sperator v-if="showItem" />
    <context-menu-item
      :label="itemText"
      :clickClose="false"
      @click="changeLabelText"
    />
  </context-menu>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import type { MenuOptions } from "@imengyu/vue3-context-menu";

export default defineComponent({
  data() {
    return {
      show: false,
      showItem: true,
      itemText: "Test item dynamic change label",
      optionsComponent: {
        x: 500,
        y: 200,
      } as MenuOptions,
    };
  },
  mounted() {
    //监听id为mx-menu-default-container的右键事件不生效
    console.log(document.getElementById("mx-menu-default-container"));
    document
      .getElementById("mx-menu-default-container")
      ?.addEventListener("contextmenu", (e) => {
        e.preventDefault();
        this.optionsComponent.x = e.x;
        this.optionsComponent.y = e.y;
        this.show = true;
      });
  },

  methods: {
    // onContextMenu(e: MouseEvent) {
    //   //prevent the browser's default menu
    //   e.preventDefault();
    //   //show our menu
    //   this.$contextmenu({
    //     x: e.x,
    //     y: e.y,
    //     items: [
    //       {
    //         label: "A menu item",
    //         onClick: () => {
    //           alert("You click a menu item");
    //         },
    //       },
    //       {
    //         label: "A submenu",
    //         children: [
    //           { label: "Item1" },
    //           { label: "Item2" },
    //           { label: "Item3" },
    //         ],
    //       },
    //     ],
    //   });
    // },
    onContextMenu(e: MouseEvent) {
      console.log(123123132);
      e.preventDefault();
      // //Set the mouse position
      this.optionsComponent.x = e.x;
      this.optionsComponent.y = e.y;
      // //Show menu
      this.show = true;
    },
    changeLabelText() {
      this.itemText =
        this.itemText == "My label CHANGED!"
          ? "Test item dynamic change label"
          : "My label CHANGED!";
    },
  },
});
</script>
<style scoped>
.box {
  width: 100%;
  height: 750px;
  background-color: brown;
}
</style>
