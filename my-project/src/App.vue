<template>
 <!-- {{isShowMore}} -->
  <div class="cards-mb-flex">
    <template v-for="(card ,key) in cards" :key="key" >
     <CardTicket :card="card" :isShow = "isShowMore[key]" />
    </template>

  </div>
 
</template>

<script>
import CardTicket from './components/CardTicket.vue'
import {ref,onMounted} from 'vue'
import {ccards} from './data/dataCard'
export default {
  name: 'App',
  components: {
    CardTicket
  },
  setup(){
    const cards = ref(ccards);
    const isShowMore = ref([]);
    // for(let i =0; i<cards.value.length;i++){
    //   isShowMore.value.push('-1')
    // }
    // console.log(isShowMore.value)
    onMounted(() => {
      
  const parentTimes = document.querySelectorAll('.card-ticket__advantage-item-times');

for(let i = 0; i<parentTimes.length;i++){
  const childTimes = parentTimes[i].querySelectorAll('.card-ticket__advantage-item-time')

  if(parentTimes[i].clientHeight>30){
    // console.log(parentTimes[i].clientHeight)
    // parentTimes[i].style.height = '30px'
    // parentTimes[i].style.overflow = 'hidden'
    console.log(parentTimes[i])
    const nums = ref(0)
    const index = ref(null)
    for(let j = 0; j <childTimes.length;j++){
   
          if((parentTimes[i].offsetWidth - 30)>nums.value){
            nums.value = nums.value+childTimes[i].offsetWidth
            console.log(nums.value + '-' +(parentTimes[i].offsetWidth - 30))
            
           if(i == childTimes.length-1){
            index.value = null;
           }
           else{
            index.value = j;
           }
          }

      
    }
if( index.value!=null){
isShowMore.value[i] = index.value -2

}
else{
  isShowMore.value[i] = index.value 
}

  }
}

})
    // const cards=ref([
    //   {
    //     advantages:['Билет на целый день','Неограниченное число катаний','6 остановок у главных достопримечательностей','Ближайший рейс сегодня'],
    //     mainImg:require('@/assets/image/Card1.svg'),
    //     time:['12:00','12:00','12:00','12:00','12:00','12:00'],
    //     sum:'900',
    //     timeClock:'2 часа',
    //     newsYellow:true,
    //     newsText:'НОВИНКА',
    //     stock: 'АКЦИЯ - Обзорная экскурсия по рекам и каналам с остановками Hop on Hop Off 2019'
    //   },
    //   {
    //     advantages:['Билет на целый день','Неограниченное число катаний','6 остановок у главных достопримечательностей','Ближайший рейс сегодня'],
    //     mainImg:require('@/assets/image/Card1.svg'),
    //     time:['12:00','12:00','12:00'],
    //     sum:'2900',
    //     sumText:'1200 р на причале dmfklsfsdfl',
    //     timeClock:'2 часа',
    //     newsPurple:true,
    //     newsText:'НОВИНКА',
    //     stock: 'АКЦИЯ - Обзорная экскурсия по рекам и каналам с остановками Hop on Hop Off 2019'
    //   },
    //   {
    //     advantages:['Билет на целый день','Неограниченное число катаний','6 остановок у главных достопримечательностей','Ближайший рейс сегодня'],
    //     mainImg:require('@/assets/image/Card5.svg'),
    //     time:['12:00'],
    //     sum:'900',
    //     sumText:'1200 р на причале',
    //     timeClock:'2 часа',
    //     newsBlue:true,
    //     newsText:'НОВИНКА'
    //   },{
    //     advantages:['Билет на целый день','Неограниченное число катаний','6 остановок у главных достопримечательностей','Ближайший рейс сегодня'],
    //     mainImg:require('@/assets/image/Card4.svg'),
    //     time:['12:00','12:00','12:00','12:00','12:00','12:00','12:00','12:00','12:00','12:00','12:00'],
    //     sum:'900',
    //     sumText:'1200 р на причале',
    //     timeClock:'2 часа',
    //     newsYellow:true,
    //     newsText:'КРУГЛЫЙ ГОД'
    //   },
    //   {
    //     advantages:['Билет на целый день','Неограниченное число катаний','6 остановок у главных достопримечательностей','Ближайший рейс сегодня'],
    //     mainImg:require('@/assets/image/Card3.svg'),
    //     time:['12:00','12:00','12:00','12:00','12:00','12:00'],
    //     sum:'900',
    //     sumText:'1200 р на причале',
    //     timeClock:'2 часа'
    //   }

    // ])
    return{
      cards,
      ccards,
      isShowMore
    }
  }
}
</script>
