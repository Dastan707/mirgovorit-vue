<template>
<div>
 <div class="wrapper">
   <div v-show="!mobileView" class="nav">
     <Navbar />
   </div>
   <div class="navbar-mobile">
     <img class="logo-img" src="@/assets/logo.png" alt="logo">
     <i @click="toggleMobileNav" v-show="mobileView" class="far fa-bars"></i>
   </div>
   <div class="main-section">
     <div class="main-section__title">
       <div class="title-left">
         <h1 class="title-left__showcase">Витрина</h1>
         <h1 class="title-left__seminars">Семинары и курсы</h1>
       </div>
       <div class="title-right">
         <h4 class="title-right__study">Моё обучение</h4>
       </div>
     </div>
     <div class="main-section__author">
     <div class="section-author__info">
       <p class="author-topic">{{author.topic}}</p>
       <p class="author-name">{{author.name}}</p>
       <p class="author-desc">{{author.description}}</p>
     </div>
     <div class="section-author__img">
       <img class="author-img" :src="author.avatar" alt="avatar">
     </div>
     </div>
     <div class="main-section__cards">
       <div v-for="card in cards" :key="card.id" class="card-item">
         <div>
         <h3>{{card.title}}</h3>
         <div class="card-item__type" v-if="card.type == 'training'">
           <img class="type-img" src="@/assets/training.svg" alt="training">
           <p>Повышение квалификации</p>
         </div>
         <div class="card-item__type" v-else-if="card.type == 'seminar'">
           <img class="type-img" src="@/assets/seminar.svg" alt="seminar">
           <p>Семинар</p>
         </div>
         <div class="card-item__time" v-if="card.duration">
           <img class="type-img" src="@/assets/time.svg" alt="time">
           <p v-if="card.duration >= 5">{{card.duration}} месяцев</p>
           <p v-else>{{card.duration}} месяца</p>
         </div>
         <div class="card-item__date" v-if="card.dateStart">
           <img class="type-img" src="@/assets/date.svg" alt="date">
           <p>Сессия {{new Date(card.dateStart).toLocaleDateString()}}</p>
         </div>
         <div v-if="card.description" class="card-item__description">
           {{card.description}}
         </div>
         <div class="card-item__curators" v-if="card.curators">
           <p>Куратор:{{card.curators.join(', ')}}</p>
         </div>
         <div class="card-item__methodists" v-else-if="card.methodists">
           <p>Методисты:{{card.methodists.join(', ')}}</p>
         </div>
         </div>
         <div class="card-item__price">
           <button v-if="card.type == 'seminar'" class="button-seminar">{{card.price}} P</button>
           <button v-else-if="card.type == 'training'" class="button-training">Выбрать тариф</button>
         </div>
       </div>
     </div>
   </div>
 </div>
</div>
</template>

<script>
import axios from 'axios'
import Navbar from './Navbar.vue'
export default {
  components: {
    Navbar
  },
  name: 'MainPage',
  data () {
    return {
      cards: [],
      author: {},
      mobileView: null,
      mobileNav: null,
      windowWidth: null
    }
  },
  methods: {
    toggleMobileNav () {
      this.mobileNav = !this.mobileNav
    },
    checkScreen () {
      this.windowWidth = window.innerWidth
      if (this.windowWidth <= 640) {
        this.mobileView = true
        return
      }
      this.mobileView = false
      this.mobileNav = false
      // eslint-disable-next-line
      return
    }
  },
  async mounted () {
    await axios.get('https://eg-cdn.s3.eu-central-1.amazonaws.com/static/fe-test/seminars-test-data.json')
      .then((res) => {
        console.log(res.data)
        this.cards = res.data.seminars
        this.author = res.data.author
      })
      .catch(error => {
        console.log(error)
      })
  },
  updated () {
    window.addEventListener('resize', this.checkScreen())
    this.checkScreen()
  }
}
</script>

<style>
body{
  font-family: "Inter", Arial, Helvetica, sans-serif;
}
.wrapper{
  display: flex;
}
.main-section{
  padding: 0 2rem;
}
.main-section__title{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.title-left{
  display: flex;
}
.title-left__showcase{
  font-family: "Inter", Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 36px;
  line-height: 48px;
}
.title-left__seminars{
  margin-left: 16px;
  font-style: normal;
  font-weight: bold;
  font-size: 36px;
  line-height: 48px;
  color: #C4C4C4;
}
.title-right__study{
  color: #007FF4;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 24px;
  text-align: right;
}
.main-section__author{
  display: flex;
  align-items: center;
  margin-bottom: 24px;
}
.section-author__info{
  width: 464px;
  height: 176px;
}
.author-img{
  width: 120px;
  height: 120px;
  border-radius: 50%;
}
.author-topic{
  width: 110px;
  height: 7px;
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
  line-height: 16px;
  letter-spacing: 1px;
  text-transform: uppercase;
}
.author-name{
  width: 418px;
  height: 16px;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 32px;
}
.author-desc{
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 24px;
}
.main-section__cards{
  display: flex;
  flex-wrap: wrap;
}
.card-item{
  width: 224px;
  height: 320px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  background-color: #FFFFFF;
  border: 1px solid #EDEDED;
  box-sizing: border-box;
  box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.03);
  border-radius: 8px;
  margin: 12px;
}
.card-item__type{
  width: 192px;
  height: 30px;
  display: flex;
  flex-direction: row;
  align-items: center;
  margin: 3px 0px;
  font-size: 14px;
  line-height: 20px;
  padding: 0px;
}
.card-item__time{
  width: 192px;
  height: 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
  font-size: 14px;
  line-height: 20px;
  padding: 0px;
}
.card-item__date{
  width: 192px;
  height: 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
  font-size: 14px;
  line-height: 20px;
  padding: 0px;
}
.card-item__description{
  font-size: 12px;
  padding: 6px;
  width: 192px;
}
.card-item__curators, .card-item__methodists{
  width: 192px;
  height: 25px;
  font-size: 12px;
  line-height: 16px;
  padding: 6px;
}
.card-item__price{
  width: 192px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: flex-end;
}
.type-img{
  margin: 0 10px;
}
.button-seminar{
  width: 92px;
  height: 32px;
  background-color: #FBAD00;
  border-radius: 8px;
  border: 0px white;
  color: #FFFFFF;
}
.button-training{
  width: 142px;
  height: 32px;
  background-color: #007FF4;
  color: #FFFFFF;
  border-radius: 8px;
  border: 0px white;
}
.navbar-mobile{
  display: flex;
  justify-content: space-between;
  padding: 0px 30px;
  align-items: center;
  top: 0;
  cursor: pointer;
}
@media all and (max-width: 640px) {
  i{
    display: block;
  }
  .wrapper{
    display: flex;
    flex-direction: column;
  }
  .main-section__title{
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }
  .title-left{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  .title-left__showcase{
    font-size: 24px;
    line-height: 32px;
  }
  .title-left__seminars{
    margin-left: 0px;
    font-size: 16px;
    line-height: 24px;
  }
  .main-section__cards{
    display: flex;
    flex-direction: column;
  }
}

</style>
