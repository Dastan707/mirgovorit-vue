<template>
  <div>
    <div class="navbar">
      <div class="navbar-logo">
       <img class="logo-img" src="@/assets/logo.png" alt="logo">
      </div>
      <div class="navbar-list">
        <div class="navbar-list__item">
        <h4>Мой кабинет</h4>
        <img src="@/assets/arrowRight.svg" alt="arrow">
        </div>
        <div @click="navbarItem = !navbarItem" class="navbar-list__item">
          <h4>Обучение</h4>
          <img v-if="navbarItem" src="@/assets/arrowDown.svg" alt="arrowDown">
          <img v-else src="@/assets/arrowRight.svg" alt="arrow">
        </div>
        <div class="navbar-item__block" v-show="navbarItem">
        <div class="navbar-item__list">
          <p>Семинары и курсы</p>
        </div>
        <div class="navbar-item__list">
          <p>Вебинары</p>
        </div>
        <div class="navbar-item__list">
          <p>Самообучение</p>
        </div>
        <div class="navbar-item__list">
          <p>Тьютор</p>
        </div>
        </div>
        <div class="navbar-list__item">
          <h4>Чат</h4>
        </div>
        <div class="navbar-list__item">
          <h4>Конкурсы</h4>
        </div>
        <div class="navbar-list__item">
          <h4>Онлайн преподавание</h4>
        </div>
        <div class="navbar-list__item">
          <h4>Маркет</h4>
        </div>
        <div class="navbar-list__item">
          <h4>Правила</h4>
        </div>
        <div class="navbar-list__item">
          <h4>Представители</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  data () {
    return {
      navbarItem: null
    }
  }
}
</script>

<style>
.navbar{
  width: 320px;
  height: 1024px;
  background-color: #f5f5f5;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  position: absolute;
}
.navbar-logo{
  display: flex;
  justify-content: center;
}
.logo-img{
    margin: 12px 0px 36px 0px;
}
.navbar-list{
  display: flex;
  flex-direction: column;
  padding: 0 2rem;
}
.navbar-list__item{
  max-width: 320px;
  max-height: 32px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: "Inter", Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 24px;
}
.navbar-item__list{
  padding: 0 1rem;
  width: 320px;
  height: 20px;
  font-family: "Inter", Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 24px;
}
.navbar-item__block{
    margin-bottom: 10px;
}
.navbar-arrow{
  width: 24px;
  height: 24px;
}
@media all and (max-width: 640px){
    .navbar{
        display: none;
    }
}
</style>
