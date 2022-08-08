<template>
  <div id="app">
    <h1>ToDoList</h1>
    <add-list
      :editname="editname"
      :item="item"
      @addList="AddItem"
      @changeList="EditItem"
    />
    <list-nav :nowtab="nowtab" @TabSwitch="TabChange" />
    <div class="list-group" v-for="i in ListFilter" :key="i.id">
      <to-do-item
        :item="item"
        :labelid="i.id"
        :labelname="i.name"
        :labeldone="i.completed"
        @editList="Edit"
        @removeList="Remove"
        @BoolChanged="ItemUpdate"
      />
    </div>
  </div>
</template>

<script>
import ToDoItem from "./components/ToDoItem";
import AddList from "./components/AddList";
import ListNav from "./components/ListNav";
export default {
  name: "App",
  components: {
    ToDoItem,
    AddList,
    ListNav,
  },
  data() {
    return {
      item: [
        {
          id: 1,
          name: "9:00打工",
          completed: false,
        },
        {
          id: 2,
          name: "帶狗狗去散步",
          completed: true,
        },
      ],
      nowtab: "ALL",
      editname: {},
      arrlength: 2,
    };
  },
  methods: {
    AddItem(value) {
      this.item.push({
        id: this.arrlength + 1,
        name: value,
        completed: false,
      });
      this.arrlength++;
    },
    EditItem(value) {
      const index = this.item.findIndex((list) => list.id === value.id);
      this.item[index] = value;
    },
    Edit(value) {
      const index = this.item.findIndex((list) => list.id === value);
      this.editname = this.item[index];
    },
    Remove(value) {
      const i = this.item.findIndex((list) => list.id === value);
      this.item.splice(i, 1);
    },
    ItemUpdate(value) {
      this.item = value;
    },
    TabChange(value) {
      this.nowtab = value;
    },
  },
  computed: {
    ListFilter() {
      if (this.nowtab == "DONE") {
        const donefilter = this.item.filter((i) => i.completed);
        return donefilter;
      } else if (this.nowtab == "TODO") {
        const undonefilter = this.item.filter((i) => !i.completed);
        return undonefilter;
      }
      return this.item;
    },
  },
  // watch: {
  //   item: {
  //     handler(val) {
  //       var itemstorage;
  //       for (var i = 0; i < val.length; i++) {
  //         console.log(val[i].id);
  //         console.log(`${val[i].id},`);
  //         itemstorage += JSON.parse(`${val[i].id},`);
  //       }
  //       localStorage.setItem("id", itemstorage);
  //     },
  //     deep: true,
  //   },
  // },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  padding: 3% 15%;
  background-color: #547b68;
}
body,
html {
  background-color: #547b68;
}
h1 {
  color: #e15b67;
}
.nav-link,
.nav-pills .nav-link.active,
.nav-pills .show > .nav-link {
  color: #ffffff !important;
  border: #ffffff 1px solid !important;
  margin-right: 10px;
}
@media (max-width: 820px) {
  #app {
    padding: 5% 5%;
  }
}
</style>
