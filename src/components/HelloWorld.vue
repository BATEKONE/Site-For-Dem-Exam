<template>
  <div class="header">
    <div class="sub-header1">
      <div style="display: flex">
        <img src="../assets/Vector.svg" alt="">
        <h1 class="header-head1">Вариант 9</h1>
      </div>
      <h2 class="header-head">Все файлы</h2>
      <h3 class="header-head">Избранное</h3>
      <h4 class="header-head">Корзина</h4>
    </div>
    <div class="sub-header2">
      <img src="../assets/Vector2.svg" alt="">
    </div>
  </div>

  <div class="main-header">
    <div class="main-header1">
      <div class="main-subheader">
        <p>PDF</p>
        <img src="../assets/Icon.svg" alt="">
      </div>
      <div class="main-subheader">
        <p>DOC</p>
        <img src="../assets/Icon.svg" alt="">
      </div>
      <div class="main-subheader">
        <p>XLS</p>
        <img src="../assets/Icon.svg" alt="">
      </div>
      <div class="main-subheader2">
        <p>PNG</p>
      </div>
    </div>
    <div class="main-header2">
      <select v-model="selectedItem">
        <option v-for="item in items" :key="item.id" :value="item">{{ item.name }}</option>
      </select>
    </div>
  </div>

  <div class="main">
    <div class="sub-main" v-for="product in products" :key="product.id">
      <div class="sub-main1">
        <img :src="product.img" alt="">
      </div>
      <div class="sub-main2">
        <h1>{{ getProductInfo(product.id) }}</h1>
        <p>{{ product.name }}</p>
        <p>{{ product.prop}}</p>
      </div>
    </div>
  </div>

  <div class="footer">
    <p>© Вариант 9. Медведев Святослав, группа ПИ-20-2</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data(){
    return{
      jsonData: null,
      items: [
        { id: 1, name: 'По умолчанию' },
        { id: 2, name: 'Избранное' },
        { id: 3, name: 'По алфавиту' }
      ],
      products: [
        {id: 1, img: require('../assets/1.svg'),
          name: 'Создал: Святослав Медведев',
          prop: 'Последние изменения год назад'},
        {id: 2, img: require('../assets/2.svg'),
          name: 'Создал: Святослав Медведев',
          prop: 'Последние изменения год назад'},
        {id: 3, img: require('../assets/3.svg'),
          name: 'Создал: Святослав Медведев',
          prop: 'Последние изменения год назад'},
        {id: 4, img: require('../assets/4.svg'),
          name: 'Создал: Святослав Медведев',
          prop: 'Последние изменения год назад'},
      ],
    }

  },
  mounted() {
    axios
        .get('https://jsonplaceholder.typicode.com/comments')
        .then(response => {
          this.jsonData = response.data;
        })
        .catch(error => {
          console.error('Ошибка при получении JSON:', error);
        });
  },

  methods: {
    getProductInfo(productId) {
      if (this.jsonData === null) {
        return '';
      }

      const item = this.jsonData.find(item => item.id === productId);
      return item ? item.name : 'Unknown';
    }
  },
}
</script>

<style scoped lang="scss">
.footer p{
  color: #667085;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  padding: 24px 50px;
}

.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 20px;
  text-align: left;
}

.sub-main1 img{
  width: 75px;
  height: 94px;
}

.sub-main2 h1{
  color: #0D1421;
  font-weight: 600;
  font-size: 18px;
  line-height: 28px;
  word-wrap: break-word;
}

.sub-main2 p{
  color: #667085;
  font-weight: 400;
  font-size: 14px;
  line-height: 20px;
  word-wrap: break-word;
}

.sub-main{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  column-gap: 35px;
}

.main {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 20px;
  padding: 0 50px;
}

.main > div {
  padding: 35px 0 0 0;
  width: calc(33.33% - 20px);
}

.main-subheader p{
  color: #fff;
  font-weight: 600;
  font-size: 14px;
  line-height: 20px;

}

.main-subheader2 p{
  color: #000;
  font-weight: 600;
  font-size: 14px;
  line-height: 20px;
}

.main-subheader img{
  width: 10px;
  height: 10px;
}

.main-subheader{
  display: flex;
  align-items: center;
  background: #0D1421;
  border-radius: 8px;
  padding: 10px 16px;
  gap: 8px;
}

.main-header1{
  display: flex;
  align-items: center;
  column-gap: 20px;
}

.main-header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 50px;
}

.header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 50px;
}

.header .sub-header1{
  display: flex;
  justify-content: space-between;
  align-items: center;
  column-gap: 40px;
}

.header .sub-header1 div{
  column-gap: 16px;
}

.header-head1{
  font-weight: 600;
  font-size: 24px;
  line-height: 32px;
}

.header-head{
  color: #0D1421;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
}

img{
  width: 32px;
  height: 32px;
}

</style>
