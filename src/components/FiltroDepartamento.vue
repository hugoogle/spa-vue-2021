<template>
  <ul class="menu__list r-list">
    <li
      class="menu__group"
      v-for="(departamento, index) in listaDepartamentos"
      v-bind:key="index"
    >
      <router-link
        to="/"
        href="#0"
        @click.prevent="filtrarDepartamento(departamento)"
        class="menu__link r-link text-underlined"
      >
        <a @click.prevent="filtrarDepartamento(departamento)">{{
          departamento
        }}</a>
      </router-link>
    </li>
  </ul>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import ProdutoStore from "../store/Store";

@Component
export default class FiltroDepartamento extends Vue {
  private departamentos = [
    "Todos os departamentos",
    "Hortifruti",
    "Bebidas",
    "Mercearia",
    "Padaria",
    "Congelado",
  ];

  get listaDepartamentos(): string[] {
    return this.departamentos;
  }

  filtrarDepartamento(departamento: string): void {
    ProdutoStore.listaPorDepartamento(departamento);
  }
}
</script>

<style scoped>
.r-link {
  display: var(--rLinkDisplay, inline-flex) !important;
}

.r-link[href] {
  color: var(--rLinkColor) !important;
  text-decoration: var(--rLinkTextDecoration, none) !important;
}

.r-list {
  padding-left: var(--rListPaddingLeft, 0) !important;
  margin-top: var(--rListMarginTop, 0) !important;
  margin-bottom: var(--rListMarginBottom, 0) !important;
  list-style: var(--rListListStyle, none) !important;
}

.menu {
  --rLinkColor: #156f96;
}

.menu__link {
  display: var(--menuLinkDisplay, block);
}

.menu:hover .menu__link:not(:hover) {
  --rLinkColor: var(--menuLinkColorUnactive, rgba(22, 22, 22, 0.35));
}

.menu__list {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px 0px 0px 0px;
}

.menu__link {
  padding: var(--menuLinkPadding, 0.5rem 2.3rem);
  font-weight: 300;
  font-weight: bold;
}

.text-underlined {
  position: relative;
  overflow: hidden;

  will-change: color;
  transition: color 0.25s ease-out;
}

.text-underlined::before,
.text-underlined::after {
  content: "";
  width: 0;
  height: 3px;
  background-color: #156f96;

  will-change: width;
  transition: width 0.1s ease-out;

  position: absolute;
  bottom: 0;
}

.text-underlined::before {
  left: 50%;
  transform: translateX(-50%);
}

.text-underlined::after {
  right: 50%;
  transform: translateX(50%);
}

.text-underlined:hover::before,
.text-underlined:hover::after {
  width: 100%;
  transition-duration: 0.2s;
  cursor: pointer;
}

.a-box {
  display: inline-block;
  width: 240px;
  text-align: center;
}

.img-container {
  height: 230px;
  width: 200px;
  overflow: hidden;
  border-radius: 0px 0px 20px 20px;
  display: inline-block;
}

.img-container img {
  transform: skew(0deg, -13deg);
  height: 250px;
  margin: -35px 0px 0px -70px;
}

.inner-skew {
  display: inline-block;
  border-radius: 20px;
  overflow: hidden;
  padding: 0px;
  transform: skew(0deg, 13deg);
  font-size: 0px;
  margin: 30px 0px 0px 0px;
  background: #c8c2c2;
  height: 250px;
  width: 200px;
}

.text-container {
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.2);
  padding: 120px 20px 20px 20px;
  border-radius: 20px;
  background: #fff;
  margin: -120px 0px 0px 0px;
  line-height: 19px;
  font-size: 14px;
}

.text-container h3 {
  margin: 20px 0px 10px 0px;
  color: #04bcff;
  font-size: 18px;
}

@media screen and (max-width: 768px) {
  .menu__list {
    flex-direction: column;
    text-align: center;
  }
}
</style>
