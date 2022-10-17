<template>
  <div class="card-ticket">
    <div class="card-ticket__main-img">
      <div class="card-ticket__billet_blue" v-if="card?.newsBlue">{{card?.newsText}}</div>
      <div class="card-ticket__billet_yellow" v-if="card?.newsYellow">{{card?.newsText}}</div>
      <div class="card-ticket__billet_purple" v-if="card?.newsPurple">{{card?.newsText}}</div>
      <!-- <img :src="card.mainImg"> -->
      <div class="card-ticket__main-img-bg" :style="`--my-src: url(${card.mainImg})`"></div>
    </div>
    <div class="card-ticket__container">
      <div>
        <div class="card-ticket__duration-stock-flex">
        <div class="card-ticket__duration">
          <img src="../assets/image/clock.svg" class="card-ticket__clock">
          <div class="card-ticket__clock-time">{{card.timeClock}}</div>
        </div>
        <div class="card-ticket__stock" v-if="card?.stock">
          {{card?.stock}}
        </div>
        </div>
        <div class="card-ticket__advantage">

          <div class="card-ticket__advantage-item" v-for="(advantag,index) in card.advantages" :key="index"
            :class="{'card-times':(card.advantages.slice(-1) == advantag)}">
            <div class="card-ticket__advantage-item_flex">
              <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg"
                class="card-ticket__check">
                <path
                  d="M7.24255 13.4204C6.51714 14.1458 5.3401 14.1458 4.61504 13.4204L0.544058 9.34932C-0.181353 8.62425 -0.181353 7.44718 0.544058 6.7221C1.26912 5.99668 2.44616 5.99668 3.17157 6.7221L5.59708 9.14731C5.78018 9.33007 6.07742 9.33007 6.26087 9.14731L12.8284 2.57961C13.5535 1.85418 14.7305 1.85418 15.4559 2.57961C15.8043 2.92797 16 3.40061 16 3.89322C16 4.38582 15.8043 4.85847 15.4559 5.20683L7.24255 13.4204Z"
                  fill="#FECF01" />
              </svg>
              <div class="card-ticket__advantage-item-text">{{advantag}}
              </div>
            </div>
            <template v-if="card.advantages.slice(-1) == advantag">
              <div class="card-ticket__advantage-item-times">
                <template v-for="(time,index) in card.time" :key="index">

                  <div class="card-ticket__advantage-item-time" @click="choseTicket"
                    :class="{' hidden-block':(index>isShow)}">
                    {{time}}
                  </div>
                  <!-- <div class="card-ticket__advantage-item-time" v-if="index<isShow" @click="choseTicket">
                  {{time}}
                </div>
                <div class="card-ticket__advantage-item-time hidden-block" v-else @click="choseTicket">
                  {{time}}
                </div> -->
                </template>
                <div class="card-ticket__advantage-item-time" v-if="(isShow||isShow==0)&&isShowMore&&card.time.length>3"
                  @click="showMore">
                  еще...</div>
              </div>
            </template>
          </div>
        </div>
      </div>
      <div class="card-ticket__bottom">
        <div class="card-ticket__price">
          <div class="card-ticket__price-flex">{{card.sum}}<img src="../assets/image/ruble_currency_icon_215811.svg"
              class="card-ticket__price-img">
          </div>
          <div class="card-ticket__price-text" v-if="card?.sumText">{{card.sumText}}
          </div>
        </div>
        <a href="#" class="card-ticket__more">
          Подробнее
        </a>
      </div>




    </div>
  </div>
</template>
<script>
import { ref, onMounted } from 'vue'
export default {
  name: 'CardTicket',
  props: {
    card: Object,
    isShow: Boolean,
    index: Number
  },
  setup(props) {
    const isShowMore = ref(true)
    const showMore = (item) => {
      const parent = item.currentTarget.closest('.card-ticket__advantage-item-times');
      const hiddenBlock = parent.querySelectorAll('.hidden-block');
      for (let i = 0; i < hiddenBlock.length; i++) {
        hiddenBlock[i].classList.remove('hidden-block');
      }
      item.currentTarget.classList.add('hidden-block');
    }
    const arrayTicket = ref([])
    const choseTicket = (item) => {
      const parent = item.currentTarget.closest('.card-ticket__advantage-item-times');
      const hiddenBlock = parent.querySelectorAll('.card-ticket__advantage-item-time');
      for (let i = 0; i < hiddenBlock.length; i++) {
        if (!hiddenBlock[i].classList.contains('hidden-block')) {
          hiddenBlock[i].classList.remove('choose-ticket')
        }

      }
      item.currentTarget.classList.add('choose-ticket')
    }

    onMounted(() => {
      //   const parentTimes = document.querySelector('.card-ticket__advantage-item-times');
      //   console.log(parentTimes)


    })
    return {
      isShowMore,
      showMore,
      choseTicket,
      arrayTicket,
      props,

    }
  }
}
</script>