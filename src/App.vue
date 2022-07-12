<template>
  <main>
    <GoodsSection v-if="goodsList.length > 0" :goods="goodsList" @deleteGood="this.deleteGood" @addGood="addGood"></GoodsSection>
  </main>
</template>

<script>
  import GoodsSection from './components/GoodsSection.vue';
  //вот этот testArray
  import testArray from './utils';

  // console.log(testArray);

  export default {
    data() {
      return {
        goodsList: [],

      }
    },
    //по-хорошему для реактивных изменений надо использовать watch, но я не понимаю,
    //как его использовать на массиве, с которого отрисовываются отвары,
    //потому что для изменения отрисовки надо поменять сам массив,
    //как в методе deleteGood
    // watch: {
    //   goodsList(newGoods, pastGoods) {
    //     console.log(newGoods, pastGoods);
    //   }
    // },
    components: {
      GoodsSection,
    },
    methods: {
      //вот здесь
      deleteGood(goodData) {
        this.goodsList = this.goodsList.filter((good) => {
          return good.id !== goodData.id;
        });
        localStorage.setItem('goodsArray', JSON.stringify(this.goodsList));
      },
      addGood(goodData) {
        this.goodsList.unshift(goodData);
        localStorage.setItem('goodsArray', JSON.stringify(this.goodsList));
      },
    },
    mounted() {
      //read операция локального хранилища
      // const testArray =  JSON.parse(localStorage.getItem('goodsArray'));
      // this.goodsList = testArray;
      
      //это массив карточек по умолчанию из файла utils.js, как заглушка. Чтобы проверить сохранение карточек при перезагрузке, нужно это закомментировать и раскомменитровать 2 строчки выше и щакомментироват импорт testArray вверху
      this.goodsList = testArray;
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: rgba(255, 254, 251, 0.8);
}
body {
  margin: 0;
}
</style>
