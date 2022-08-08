<template>
  <div class="row pt-md-2 d-flex align-items-center liststyle">
    <div class="col-1 col-md-1">
      <input
        type="checkbox"
        :checked="isDone"
        :key="labelid"
        v-model="isDone"
        @change="BoolChanged(labelid)"
      />
    </div>
    <div class="labeltext col-5 col-md-7">
      <span class="text-center" :class="{ done: isDone }">
        {{ labelname }}
      </span>
    </div>
    <div class="btngroup col-6 col-md-4">
      <button @click="editList(labelid)" class="btn me-2" type="button">
        Edit
      </button>
      <button @click="removeList(labelid)" class="btn me-2" type="button">
        Del
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDoItem",
  props: {
    item: { type: Array },
    labelid: { type: Number },
    labelname: { type: String },
    labeldone: { type: Boolean },
  },
  emits: ["editList", "removeList", "BoolChanged"],
  data() {
    return {
      todo: this.item,
      isDone: this.labeldone,
    };
  },
  methods: {
    editList(j) {
      this.$emit("editList", j);
    },
    removeList(obj) {
      this.$emit("removeList", obj);
    },
    BoolChanged(i) {
      const index = this.todo.findIndex((list) => list.id === i);
      this.todo[index].completed = !this.todo[index].completed;
      this.$emit("BoolChanged", this.todo);
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
.liststyle {
  color: #ffffff;
  border: 1px #d1b2a5 solid;
  margin-top: 10px;
  padding: 8px 0;
  border-radius: 5px 10px;
}
.labeltext {
  white-space: nowrap;
  overflow-x: hidden;
}
.btn {
  border: 1px #f1e5c9 solid;
  color: #f1e5c9;
}
.btn:hover {
  background-color: #ffffff;
  border: 1px #f1e5c9 solid;
  color: #547b68;
}
.btngroup {
  text-align: right;
}
@media (max-width: 768px) {
  .labeltext {
    white-space: nowrap;
    overflow-x: auto;
  }
}
</style>
