<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <div id="container">
        <strong class="capitalize">{{ dataArray.name }}</strong>
        <p>
          {{ dataArray.title }}
        </p>
      </div>

      <template v-if="dataArray.items">
        <div v-for="item of dataArray.items" :key="item.title">
          <img :src="item.url" :alt="item.title" />
          <p>
            {{ item.title }} <span> {{ item.price }}</span>
          </p>
        </div>
      </template>

      <div v-else>
        <img :src="dataArray.url" :alt="dataArray.title" />
        <p>
          {{ dataArray.title }} <span> {{ dataArray.price }}</span>
        </p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { IonContent, IonPage } from "@ionic/vue";

import "../constants/cardapio";
import * as data from "../constants/cardapio";

export default defineComponent({
  name: "FolderPage",
  components: {
    IonContent,
    IonPage,
  },

  mounted() {
    this.getPageObj(this.$route.params.id);
  },

  data: () => {
    return {
      dataArray: {},
    };
  },

  methods: {
    getPageObj(value: string | string[]) {
      if (value === "entradas") {
        this.dataArray = data.entradas;
      }

      if (value === "lanches") {
        this.dataArray = data.lanches;
      }

      if (value === "refeicoes") {
        this.dataArray = data.refeicoes;
      }

      if (value === "sobremesas") {
        this.dataArray = data.sobremesas;
      }

      if (value === "bebidas") {
        this.dataArray = data.bebidas;
      }

      if (value === "dia") {
        const date = new Date();
        const day = date.getDay();

        this.dataArray = data.promos.items[day];
      }
    },
  },
});
</script>

<style scoped>
#container {
  display: flex;
  flex-flow: column;
  align-items: center;
  padding: 2rem;
}

#container strong {
  font-size: 28px;
  line-height: 26px;
  padding: 1rem;
}

#container p {
  font-size: 20px;
  line-height: 22px;
  color: #070707;
  margin: 0;
}

#container a {
  text-decoration: none;
}
div vdataArray.items{
  font-size: 20px;
  align-items: center;

}
</style>
