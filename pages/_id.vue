<template>
  <div>
    <div v-for="contractor of obj.contractors" :key="contractor.name">
      <h3 class="my-4">
        {{ contractor.name }}
      </h3>
      <v-data-table
        :headers="headers"
        :items="contractor.works"
        hide-default-footer
        item-key="name"
        class="elevation-1"
      >
        <template v-slot:item.date="{ item }">
          {{ formatDate(item.date) }}
        </template>
        <template v-slot:item.dt="{ item }">
          <span v-if="!item.finish">
            <v-chip :color="rangeColor(item.dt)" outlined light>
              {{ item.dt * 100 }}%
            </v-chip>
          </span>
        </template>

        <template v-slot:item.plan="{ item }">
          {{ Math.round(item.plan * 100) }}%
        </template>

        <template v-slot:item.fact="{ item }">
          {{ Math.round(item.fact * 100) }}%
        </template>

        <template v-slot:item.week="{ item }">
          {{ Math.round(item.week * 100) }}%
        </template>

        <template v-slot:item.number="{ item }">
          <span v-if="item.number">
            <v-chip :color="getColor(item.color)" dark>
              {{ item.number }}
            </v-chip>
          </span>
        </template>
      </v-data-table>
    </div>
  </div>
</template>

<script>
import json from "../data.json";
export default {
  name: "IndexPage",
  data: () => ({
    items: json,
    id: 0,
    headers: [
      {
        text: "Work",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Дата", value: "date" },
      { text: "Дельта", value: "dt" },
      { text: "План", value: "plan" },
      { text: "Факт", value: "fact" },
      { text: "Неделя", value: "week" },
      { text: "Вопрос", value: "number" },
      { text: "Коментарий", value: "comment" },
      { text: "Описание", value: "description" },
      { text: "Последствие", value: "consequence" },
      { text: "Решение", value: "solution" },
    ],

    photos: [
      {
        obj: "https://www.rusgasdob.ru/assets/photos/gas-chemistry-complex-1.jpg",
        curator: "https://avatars0.githubusercontent.com/u/9064066?v=4&s=460",
      },
      {
        obj: "https://seanews.ru/wp-content/uploads/2021/03/gpz-ust-luga.jpg",
        curator: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
      },
      {
        obj: "https://oteca.ru/wp-content/uploads/2021/04/ust-luga.jpeg",
        curator: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
      },
      {
        obj: "https://rupec.ru/upload/iblock/2d5/2d5b183f10d93043c847516c5499249a.jpg",
        curator: "https://cdn.vuetifyjs.com/images/lists/4.jpg",
      },
    ],
  }),
  mounted() {},
  computed: {
    obj() {
      return this.items[this.$route.params.id - 1];
    },
  },
  methods: {
    rangeColor(dt) {
      if (dt < 0) return "red";
      else if (dt > 0) return "green";
      else return "black";
    },
    getColor(color) {
      if (color) {
        return "#" + color;
      } else {
        return "white";
      }
    },
    formatDate(date) {
      var d = new Date(date),
        month = "" + (d.getMonth() + 1),
        day = "" + d.getDate(),
        year = d.getFullYear();

      if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day;

      return [year, month, day].join("-");
    },
  },
};
</script>
