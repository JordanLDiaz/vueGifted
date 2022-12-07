<template>
  <div class="col-3 p-3">
    <div class="rounded elevation-2" @click="openGift(gift.id)">
      <img v-if="(gift.opened == true)" :src="gift.url" alt="gift" class="img-fluid" />
      <img v-else-if="(gift.opened == false)" class="img-fluid"
        src="https://images.unsplash.com/photo-1512909006721-3d6018887383?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTR8fGdpZnR8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60"
        alt="" />
      <h5 class="text-center p-2">{{ gift.tag }}</h5>
    </div>
  </div>
</template>


<script>
import { AppState } from '../AppState';
import { computed, reactive, onMounted } from 'vue';
import { giftsService } from "../services/GiftsService.js";

export default {
  props: { gift: Object },
  setup() {
    return {
      gifts: computed(() => AppState.gifts),

      async openGift(id) {
        try {
          await giftsService.openGift(id)
        } catch (error) {
          logger.error(error)
          Pop.error(('[ERROR]'), error.message)
        }
      }
    }
  }
};
</script>


<style lang="scss" scoped>

</style>
