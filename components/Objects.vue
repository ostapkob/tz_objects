<template>
  <v-container>
    <v-row justify="space-around">
      <v-card width="400">
        <v-img
        class="pointer"
          height="200px"
          href="#"
          @click.prevent="openLink(obj.id)"
          :src="photos.obj"
        >
          <v-app-bar flat color="rgba(0, 0, 0, 0.2)">
            <v-toolbar-title class="text-h6 white--text pl-0">
              {{ obj.name }}
            </v-toolbar-title>

            <v-spacer></v-spacer>

            <v-btn color="white" icon>
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </v-app-bar>

          <v-card-title class="white--text mt-8">
            <v-avatar size="56">
              <img alt="user" :src="photos.curator" />
            </v-avatar>
            <p class="ml-3 curator">{{ obj.curator }}</p>
          </v-card-title>
        </v-img>

        <div v-for="contractor of obj.contractors" :key="contractor.name">
          <v-card-text>
            <div class="font-weight-bold ml-8 mb-2">{{ contractor.name }}</div>

            <v-timeline align-top dense>
              <v-timeline-item
                v-for="work in contractor.works"
                :key="work.name"
                :color="getColor(work.color)"
                small
              >
                <template v-slot:icon>
                  <span class="invert--text">{{ work.number }}</span>
                </template>
                <div class="font-weight-normal">
                  <strong>{{ work.name }}</strong>
                  <v-icon v-if="work.finish" color="green"
                    >mdi-check-bold</v-icon
                  >
                </div>
                {{ formatDate(work.date) }}
                <span v-if="!work.finish" class="ml-6">
                  <span v-if="work.dt < 0">
                    {{ work.dt * 100 }}%
                    <v-icon color="red">mdi-arrow-down-thin</v-icon>
                  </span>
                  <span v-if="work.dt > 0">
                    {{ work.dt * 100 }}%
                    <v-icon color="green">mdi-arrow-up-thin</v-icon>
                  </span>
                  <span v-if="work.dt == 0"> {{ work.dt * 100 }}%</span>
                </span>
              </v-timeline-item>
            </v-timeline>
          </v-card-text>
        </div>
      </v-card>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data: () => ({}),
  props: {
    obj: Object,
    photos: Object,
  },
  methods: {
    getColor: (color) => "#" + color,
    formatDate(date) {
      var d = new Date(date),
        month = "" + (d.getMonth() + 1),
        day = "" + d.getDate(),
        year = d.getFullYear();

      if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day;

      return [year, month, day].join("-");
    },
    openLink(id) {
      this.$router.push(`/${id}`);
    },
  },
};
</script>

<style scoped>
.curator {
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0.9;
  color: #fff;
  margin: 2px;
  padding-left: 8px;
  padding-right: 8px;
  border-radius: 25px;
}
.pointer {
  cursor: pointer;
}
</style>