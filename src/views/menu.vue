<template>
  <div class="Menu">
    <b-container>
      <b-row>
        <b-col v-for="(menu, key) in list" :key="key">
          <b-card
            :img-src="menu.url"
            img-alt="Card image"
            img-left
            class="mb-3"
          >
            <h1>
              {{ (name = menu.name) }}
            </h1>
            <br />
            {{ menu.Engname }}
            <br />
            {{ menu.title }}
            <br />
            {{ menu.title1 }}
            <h2 class="mt-4">{{ menu.price }} Baht</h2>
            <b-button @click="index = key, buy()" variant="danger" class="mt-4">
              BUY
            </b-button>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
import { db } from "@/plugin/firebaseConfig.js";
export default {
  name: "menu",
  data: () => ({
    list: [],
    index:0,
    name: null,
    price: 0,
  }),
  created() {
    this.get();
  },
  methods: {
    get() {
      db.collection("FoodDetail")
        .orderBy("price")
        .onSnapshot((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            this.list.push(doc.data());
          });
        });
    },
    buy() {

      alert(this.list[this.index].name + " " + this.list[this.index].price);
    },
  },
};
</script>
