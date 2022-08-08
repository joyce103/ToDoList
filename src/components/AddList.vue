<template>
  <div class="input-group mb-3" v-if="editbool">
    <input
      @keyup.enter="addList"
      v-model.trim="content"
      type="text"
      class="form-control"
      placeholder="請輸入代辦事項"
      aria-label="請輸入代辦事項"
      aria-describedby="button-addon2"
    />
    <button @click="addList" class="btn" type="button" id="button-addon2">
      確認
    </button>
  </div>
  <div class="input-group mb-3" v-else>
    <input
      @keyup.enter="changeList"
      v-model.trim="temptext.name"
      type="text"
      class="form-control"
      aria-describedby="button-addon2"
    />
    <button @click="changeList" class="btn" type="button" id="button-addon2">
      確認
    </button>
  </div>
</template>

<script>
export default {
  name: "AddList",
  props: {
    item: { type: Object },
    editname: { type: Object },
  },
  emits: ["addList", "changeList"],
  data() {
    return {
      todo: this.item,
      content: "",
      temptext: "",
      editbool: true,
    };
  },
  methods: {
    addList() {
      if (this.content != "") {
        this.$emit("addList", this.content);
        this.content = "";
      } else {
        alert("尚未輸入內容");
      }
    },
    changeList() {
      if (this.temptext.name != "") {
        this.$emit("changeList", this.temptext);
        this.temptext = "";
        this.editbool = true;
      } else {
        alert("該欄位不可為空白");
      }
    },
  },
  watch: {
    editname(val) {
      this.temptext = { ...val };
      this.editbool = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-group > .form-control,
.input-group > .form-floating,
.input-group > .form-select {
  background-color: #f1e5c9;
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
</style>
