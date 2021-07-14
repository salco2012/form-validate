<template>
   <form class="sign-up" @submit.prevent="onSubmirForm">
      <div class="form-group">
         <label for="name">Имя:</label>
         <input class="form-control" id="name" type="text" v-model.trim="form.name">
         <p class="error" v-if="$v.form.name.$dirty && !$v.form.name.alpha">Только буквы</p>
      </div>
      <div class="form-group">
         <label for="full-name">Фамилия:</label>
         <input class="form-control" id="full-name" type="text" v-model.trim="form.fullName">
         <p class="error" v-if="$v.form.fullName.$dirty && !$v.form.fullName.alpha">Только буквы</p>
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
         <p class="error" v-if="$v.form.profession.$dirty && !$v.form.profession.maxCount">Не более 3-х вариантов</p>
      </div>
            <div class="form-group">
         <label for="email">Почта:</label>
         <input  id="email" class="form-control" type="email" v-model.trim="form.email">
         <p class="error" v-if="$v.form.email.$dirty && !$v.form.email.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.email.$dirty && !$v.form.email.email">Это не похоже на email</p>
      </div>
      <div class="form-group">
         <label for="phone">Контактный телефон:</label>
         <input class="form-control" id="phone" type="text" v-model.trim="form.phone">
         <p class="error" v-if="$v.form.phone.$dirty && !$v.form.phone.numeric">Только цифры</p>
      </div>
      <div class="form-group">
         <label for="login">Логин</label>
         <input class="form-control" id="login" type="text" v-model.trim="form.login">
         <p class="error" v-if="$v.form.login.$dirty && !$v.form.login.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.login.$dirty && !$v.form.login.alpha">Только латиница</p>
      </div>
         <div class="form-group">
         <label for="password">Пароль</label>
         <input class="form-control" id="password" type="password" v-model.trim="form.password">
         <p class="error" v-if="$v.form.password.$dirty && !$v.form.password.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.password.$dirty && !$v.form.password.minLength">Введите минимум 6 символов</p>
      </div>
      <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
   </form>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, email, numeric, helpers} from 'vuelidate/lib/validators'
const alpha = helpers.regex('alpha', /^[a-zA-Z]*$/)

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
             this.$v.form.$touch()
         }
      },
      validations: {
         form: {
            name: {
               alpha
            },
            fullName: {
               alpha
            },
            email: {
               minLength: minLength(4),
               required,
               email
            },
            phone: {
               numeric
            },
            login: {
               required,
               alpha
            },
            password: {
               minLength: minLength(6),
               required,
            },
            profession: {
               maxCount(value) {
                  return value.length <= 3
               }
            }
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
.error{
   color: red;
}
</style>