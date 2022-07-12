<template>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav> -->
  <!-- <router-view/> -->
  <main>
    <GoodsSection v-if="goodsList" :goods="goodsList" @deleteGood="this.deleteGood" @addGood="addGood"></GoodsSection>
  </main>
</template>

<script>
  import GoodsSection from './components/GoodsSection.vue';
  import goodPic from './assets/goodPic.png';
  import deleteSvg from './assets/delete.svg'; 
  export default {
    data() {
      return {
        goodsList: null,
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
        // console.log(goodData);
        // const goodIndex = this.goodsList.indexOf(goodData);
        // this.goodsList.splice(goodIndex, 1);
        // this.goodsList = resultArray;
        this.goodsList = this.goodsList.filter((good) => {
          return good.id !== goodData.id;
        });
      },
      addGood(goodData) {
        this.goodsList.unshift(goodData);
      },
    },
    mounted() {
      this.goodsList = [         
        {
          name: "Товар 1",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 10000,
          id: 1,
          pic: goodPic,
          delete: deleteSvg,
        }, 
        {
          name: "Картина",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 20000,
          id: 2,
          pic: goodPic,
          delete: deleteSvg,
        }, 
        {
          name: "Фотоаппарат",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 30000,
          id: 3,
          pic: goodPic,
          delete: deleteSvg,
        },
        {
          name: "Ноутбук",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 40000,
          id: 4,
          pic: goodPic,
          delete: deleteSvg,
        },
        {
          name: "Телефон",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 50000,
          id: 5,
          pic: goodPic,
          delete: deleteSvg,
        },    
      ];
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

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
