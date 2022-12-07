<template>
  <div class="container-fluid">
    <section class="row justify-content-center">
      <GiveAGift />
    </section>

    <section class="row">
      <!-- <div v-for="g in gifts" class="col-3 p-3">
        <div class="rounded elevation-2">
          <img :src="g.img" alt="gift" class="img-fluid" />
          <h4 class="text-center p-2">{{ g.tag }}</h4>
        </div>
      </div> -->
      <!--                                        VVVVV Name of prop being passed down -->
      <GiftDetails v-for="g in gifts" :key="g.id" :gift="g" />
    </section>
  </div>
</template>

<script>
import { onMounted, computed } from 'vue'
import { AppState } from "../AppState.js"
import { giftsService } from "../services/GiftsService.js"
import { logger } from "../utils/Logger.js"
import Pop from "../utils/Pop.js"
export default {
  setup() {
    onMounted(() => {
      getGifts()
    })

    async function getGifts() {
      try {
        await giftsService.getGifts()
      } catch (error) {
        logger.error(error)
        Pop.error(error)
      }
    }

    return {
      gifts: computed(() => AppState.gifts)
    }
  }
}
</script>

<style scoped lang="scss">
.img {

  background-position: center;
}
</style>
