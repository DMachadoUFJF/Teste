<template src="./Menu.html"></template>

<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import Notify from "@/core/notify";
import { Watch } from "vue-property-decorator";

@Component({
  name: "menu-app",
})
export default class Menu extends Vue {
  public mini = true;
  public drawer = false;
  public items: any[] = [];
  public notify = Notify();
  logoUrl = require("../../assets/logo.png");

  @Watch("mini")
  public closeAllMenu() {
    if (this.mini) {
      this.items.forEach((item) => (item.active = false));
    }
  }

  created() {
    this.items = [
      {
        icon: "mdi-home",
        "icon-alt": "mdi-chevron-down",
        text: "Home",
        allowed: true,
        action: () => this.redirect("/main")
      },
      {
        icon: "mdi-checkbox-marked-circle-outline",
        text: "Strings",
        action: () => this.redirect("/main"),
        allowed: true,
      },
      {
        icon: "mdi-checkbox-marked-circle-outline",
        text: "Estrutura de repeticao",
        action: () => this.redirect("/main"),
        allowed: true,
      },
      {
        icon: "mdi-checkbox-marked-circle-outline",
        text: "Estrutura condicional",
        action: () => this.redirect("/main"),
        allowed: true,
      },
      {
        icon: "mdi-checkbox-marked-circle-outline",
        text: "Vetores",
        action: () => this.redirect("/main"),
        allowed: true,
      },
      {
        icon: "mdi-checkbox-marked-circle-outline",
        text: "Matrizes",
        action: () => this.redirect("/main"),
        allowed: true,
      },
    ];
  }

  public redirect(url: string) {
    this.$router.push(url);
  }

  public activeDrawer() {
    this.drawer = !this.drawer;
    this.mini = !this.mini;
    this.items.forEach(function (item) {
      item.active = false;
    });
  }

  public updateTheme() {
    this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    if (this.$vuetify.theme.dark) {
      localStorage.setItem("theme", "dark");
    } else {
      localStorage.setItem("theme", "light");
    }
  }

  public notififyExample() {
    this.notify.success("Teste de notificação");
  }
}
</script>
<style lang="scss" src="./Menu.scss" scoped></style>
