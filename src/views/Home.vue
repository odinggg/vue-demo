<template>
  <div class="home">
    <Wechat/>
  </div>
</template>

<script>
// @ is an alias to /src
import Wechat from "@/components/Wechat.vue";

export default {
  name: "Home",
  components: {
    Wechat
  }
};
</script>
