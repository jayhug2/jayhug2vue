<template>
  <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
      <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
      </span>

      <Modal :show="showModal" @close="showModal = false">
        <h3 slot="header">
          경고!
          <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
        </h3>
        <div slot="body">내용을 입력하세요</div>
      </Modal>
      
  </div>
</template>

<script>
import Modal from "./common/Modal.vue";

export default {
  data: function() {
    return {
      newTodoItem:"",
      showModal:false,
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem) {
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal
      }
      
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  width:100%;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  width:80%;
  height:40px;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478Fb, #8763Fb);
  display: block;
  width: 50px;
  border-radius: 0 5px 5px 0;
  height:50px
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn{
  color: #42b983;
  float:right;
}
</style>