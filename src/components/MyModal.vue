<template>
  <button @click="open = true">Open Modal</button>
  <Teleport to="body">
    <div v-if="open" class="modal">
      <p>Hello from the modal!</p>
      <button @click="open = false">Close</button>
    </div>

  </Teleport>
  
</template>

<script>
import { ref } from 'vue'

export default {
  // name: "HelloWorld",
  props: {
    msg: String
  },
  components:{
    // TeleportedComponent:Teleport(Component)
  },
  setup(){
    const open = ref(false)
    return{
      open
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.modal {
    position: fixed;
    z-index: 999;
    top: 20%;
    left: 50%;
    width: 300px;
    margin-left: -150px;
    background: #f2ecec;
    box-shadow: 4px 3px rgb(239 239 227);
    text-align: center;
    padding: 10px;

}
</style>
