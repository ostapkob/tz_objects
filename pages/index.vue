<template>
  <div>
    <div v-for="obj of items" :key="obj.name">
      <objects :obj=obj :photos=photos[obj.id-1] />
    </div>
  </div>
</template>

<script>
import Objects from "../components/Objects.vue";
import json from "../data.json";

export default {
  components: { Objects },
  name: "IndexPage",
  data: () => ({
    items: json,
    photos: [
      {
        obj: "https://www.rusgasdob.ru/assets/photos/gas-chemistry-complex-1.jpg",
        curator: "https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
      },
      {
        obj: "https://seanews.ru/wp-content/uploads/2021/03/gpz-ust-luga.jpg",
        curator: "https://cdn.vuetifyjs.com/images/lists/1.jpg"
      },
      {
        obj: "https://oteca.ru/wp-content/uploads/2021/04/ust-luga.jpeg",
        curator: "https://cdn.vuetifyjs.com/images/lists/2.jpg"
      },
      {
        obj: "https://rupec.ru/upload/iblock/2d5/2d5b183f10d93043c847516c5499249a.jpg",
        curator: "https://cdn.vuetifyjs.com/images/lists/4.jpg"
      },
    ],
  }),
  mounted() {
    console.log("------");
    console.log(this.items);
  },
};
</script>
