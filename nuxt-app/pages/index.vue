<template>
  <div>
    <p v-for="message in messages" :key="message.id">
      {{ message.sender }}: {{ message.message }}
    </p>
  </div>
</template> <script>
import messages from "@/static/messages.json";
export default {
  data() {
    return { messages: messages.conversation };
  },
};
</script> 

<style scoped>
*{
color: white;

}
</style>