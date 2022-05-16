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
          <p>
            {{ item.title }}
            <span v-if="item.price > 0">
              {{ getCurrencyFormatted(item.price) }}</span
            >
          </p>
          <img :src="item.url" :alt="item.title" />
        </div>
      </template>

      <div v-else>
        <img :src="dataArray.url" :alt="dataArray.title" />
        <p>
          {{ dataArray.title }}
          <span> {{ getCurrencyFormatted(dataArray.price) }}</span>
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

        const promos = data.promos;
        promos.items = [data.promos.items[day]];

        this.dataArray = promos;
      }
    },
    getCurrencyFormatted(number: number) {
      var formatter = new Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "BRL",
      });

      return formatter.format(number);
    },
  },
});
</script>

<style scoped>
div {
  display: flex;
  flex-flow: column;
  align-items: center;
  padding: 1rem;
}

img {
  height: 300px;
  width: 400px;
}

p {
  font-size: 20px;
  font-family: cursive;
}

#container strong {
  font-size: 32px;
  line-height: 26px;
  padding: 0.5rem;
}

#container p {
  font-size: 24px;
  line-height: 22px;
  color: #070707;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
