<template>
   <form class="sign-up">
      <div class="form-group">
         <label for="name">Имя:</label>
         <input class="form-control" id="name" type="text">
      </div>
      <div class="form-group">
         <label for="full-name">Фамилия:</label>
         <input class="form-control" id="full-name" type="text">
      </div>
      <div class="form-group">
      <label for="сurrent-city">Город проживания:</label>
      <select class="form-select" id="сurrent-city">
         <option v-for="(city, index) in cities" :key="index">
            {{ city }}
         </option>
      </select>
      </div>
      <div class="form-group">
         <label for="profession">Профессия:</label>
         <select class="form-select" id="profession" multiple>
               <option v-for="(profession, index) in professions" :key="index">
                  {{ profession }}
               </option>
         </select>
      </div>
            <div class="form-group">
         <label for="email">Почта:</label>
         <input  id="email" class="form-control" type="text">
      </div>
      <div class="form-group">
         <label for="phone">Контактный телефон:</label>
         <input class="form-control" id="phone" type="text">
      </div>
      <div class="form-group">
         <label for="login">Логин</label>
         <input class="form-control" id="login" type="text">
      </div>
         <div class="form-group">
         <label for="password">Пароль</label>
         <input class="form-control" id="password" type="text">
      </div>
      <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
   </form>
</template>

<script>
   export default {
      name: 'Form',
      data() {
         return {
            cities: [
               'Москва',
               'Санкт-Петербург',
               'Барнаул',
               'Ярославль',
               'Белгород',
               'Ростов',
               'Ялта',
               'Инта',
               'Варкута',
               'Воронеж',
               'Ижевск',
               ],
            professions: [
               'Автослесарь',
               'Водитель скорой помощи',
               'Бухгалтер',
               'Участковый',
               'Медицинский работник',
               'Водитель такси',
               'Грузчик'
               ]
         }
      }
   }
</script>

<style scoped>
.sign-up{
   margin: 50px
}
.form-control,
.form-select{
   width: 400px;
}
.form-group{
   margin-bottom: 15px;
}
label{
   margin-bottom: 5px;
}
</style>