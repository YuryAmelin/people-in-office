<template>
  <div id="app" @click="closePersonCard">
    <div class="office">
      <Map @select="handleClick" />
      <SideMenu :person="this.selectedPerson" :is-user-openned="isOpened" />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import people from "./assets/data/people.json";

export default {
  name: "App",
  components: {
    Map,
    SideMenu,
  },
  data: () => ({
    selectedPerson: null,
    isOpened: false,
    people: [],
    close: null,
  }),
  created() {
    this.loadPeople();
  },
  methods: {
    loadPeople() {
      this.people = people;
    },
    closePersonCard() {
      if (this.close) {
        this.isOpened = false;
      } else {
        this.close = true;
      }
    },
    handleClick(tableId) {
      this.close = false;
      this.selectedPerson = this.people.find((it) => it.tableId === tableId);
      this.isOpened = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
