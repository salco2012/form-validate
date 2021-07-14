<template>
   <form class="sign-up" @submit.prevent="onSubmirForm">
      <div class="form-group">
         <label for="name">Имя:</label>
         <input class="form-control" id="name" type="text" v-model.trim="form.name">
      </div>
      <div class="form-group">
         <label for="full-name">Фамилия:</label>
         <input class="form-control" id="full-name" type="text" v-model.trim="form.fullName">
      </div>
      <div class="form-group">
      <label for="сurrent-city">Город проживания:</label>
      <select class="form-select" id="сurrent-city" v-model="form.city">
         <option 
         v-for="(city, index) in cities" 
         :key="index" :value="city.value">
            {{ city.label }}
         </option>
      </select>
      </div>
      <div class="form-group">
         <label for="profession">Профессия:</label>
         <select class="form-select" id="profession" v-model="form.profession" multiple>
               <option 
               v-for="(profession, index) in professions" 
               :key="index"
               :value="profession.value"
               >
                  {{ profession.label }}
               </option>
         </select>
      </div>
            <div class="form-group">
         <label for="email">Почта:</label>
         <input  id="email" class="form-control" type="email" v-model.trim="form.email">
      </div>
      <div class="form-group">
         <label for="phone">Контактный телефон:</label>
         <input class="form-control" id="phone" type="text" v-model.trim="form.phone">
      </div>
      <div class="form-group">
         <label for="login">Логин</label>
         <input class="form-control" id="login" type="text" v-model.trim="form.login">
      </div>
         <div class="form-group">
         <label for="password">Пароль</label>
         <input class="form-control" id="password" type="password" v-model.trim="form.password">
      </div>
      <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
   </form>
</template>

<script>
import { validationMixin } from 'vuelidate'

   export default {
      mixins: [validationMixin],
      name: 'Form',
      data() {
         return {
            form: {
               name: '',
               fullName: '',
               profession: ['Car mechanic'],
               city: 'Moscow',
               email: '',
               phone: '',
               login: '',
               password: ''
            },
            cities: [
               {label: 'Москва',
               value: 'Moscow'
               },
               {label: 'Санкт-Петербург',
               value: 'St. Petersburg'
               },
               {label: 'Барнаул',
               value: 'Barnaul'
               },
               {label: 'Ярославль',
               value: 'Yaroslavl'
               },
               {label: 'Белгород',
               value: 'Belgorod'
               },
               {label: 'Ростов',
               value: 'Rostov'
               },
               {label: 'Ялта',
               value: 'Yalta'
               },
               {label: 'Инта',
               value: 'Inta'
               },
               {label: 'Воркута',
               value: 'Vorkuta'
               },
               {label: 'Воронеж',
               value: 'Voronezh'
               },
               {label: 'Ижевск',
               value: 'Izhevsk'
               },
               ],
            professions: [
                {label: 'Автослесарь',
                value: 'Car mechanic'
                },
               {label: 'Водитель скорой помощи',
                value: 'Ambulance driver'
                },
               {label: 'Бухгалтер',
                value: 'Accountant'
                },
               {label: 'Участковый',
                value: 'Precinct'
                },
               {label: 'Медицинский работник',
                value: 'Medical worker'
                },
               {label: 'Водитель такси',
                value: 'Водитель такси'
                },
               {label: 'Грузчик',
                value: 'Loader'
                },
               ]
         }
      },
      methods: {
         onSubmirForm() {

         }
      },
      validations: {
         form: {
            
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