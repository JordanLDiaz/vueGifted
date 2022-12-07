<template>
  <div class="col-12">
    <div class="bg-dark text-light rounded m-2 p-3">
      <h4 class="text-center">Gifted</h4>
      <h5 class="text-center">Join the joy of gift giving!</h5>
      <form action="" class="input-group" @submit.prevent="createGift">
        <p class="p-2">TAG :</p>
        <input class="form-control form-control-md" type="text" placeholder="Input gift message" id="tag" name="tag"
          required v-model="giftForm.tag">
        <p class="p-2">URL :</p>
        <input class="form-control form-control-md" type="text" placeholder="input image url" id="url" name="url"
          required v-model="giftForm.url">
        <button class="bg-info lighten text-white m-2 px-3 fs-5 rounded"> Submit </button>
      </form>
    </div>
  </div>
</template>


<script>
import { AppState } from '../AppState';
import { computed, reactive, onMounted } from 'vue';
import { giftsService } from "../services/GiftsService.js";
import Pop from "../utils/Pop.js";
import { logger } from "../utils/Logger.js";
import { giftApi } from "../services/AxiosService.js";

export default {
  props: { gift: Object },

  setup() {

    const giftForm = reactive({
      tag: '',
      url: ''
    })

    return {
      gifts: computed(() => AppState.gifts),

      async createGift() {
        try {
          window.event.preventDefault()
          logger.log("creating gift")
          await giftsService.createGift()
        } catch (error) {
          logger.error(error)
          Pop.error(error)
        }
      }
    }
  }
};
</script>


<style lang="scss" scoped>

</style>