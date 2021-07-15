<template>
   <form class="sign-up" @submit.prevent="onSubmirForm" novalidate>
      <div class="form-group">
         <label for="name">Имя:</label>
         <input class="form-control" id="name" type="text" v-model.trim="form.name"
         :class="{'is-invalid bg-input-error' : $v.form.name.$error}">
         <p class="error" v-if="$v.form.name.$dirty && !$v.form.name.alphaRus">Только кириллица</p>
      </div>
      <div class="form-group">
         <label for="full-name">Фамилия:</label>
         <input class="form-control" id="full-name" type="text" v-model.trim="form.fullName"
         :class="{'is-invalid bg-input-error' : $v.form.fullName.$error}">
         <p class="error" v-if="$v.form.fullName.$dirty && !$v.form.fullName.alphaRus">Только кириллица</p>
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
         <select class="form-select" id="profession" v-model="form.profession" multiple
         :class="{'is-invalid bg-input-error' : $v.form.profession.$error}">
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
         <label for="email">Почта: <span class="text-danger">*</span> </label>
         <input  id="email" class="form-control" type="email" 
         v-model.trim="form.email"
         :class="{'is-invalid bg-input-error' : $v.form.email.$error}"
         >
         <p class="error" v-if="$v.form.email.$dirty && !$v.form.email.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.email.$dirty && !$v.form.email.email">Это не похоже на email</p>
      </div>
      <div class="form-group">
         <label for="phone">Контактный телефон <span class="text-danger">*</span></label>
         <input class="form-control" id="phone" type="text" 
         placeholder="+7 (921) 123-45-67"
         v-imask="form.mask"
         v-model.trim="form.phone"
          @accept="onAccept"
          @complete="onComplete"
         :class="{'is-invalid bg-input-error' : $v.form.phone.$error}"
         >
         <p class="error" v-if="$v.form.phone.$dirty && !$v.form.phone.required">Обязательное поле</p>
      </div>
      <div class="form-group">
         <label for="login">Логин <span class="text-danger">*</span> </label>
         <input class="form-control" id="login" type="text" 
         v-model.trim="form.login"
         :class="{'is-invalid bg-input-error' : $v.form.login.$error}"
         >
         <p class="error" v-if="$v.form.login.$dirty && !$v.form.login.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.login.$dirty && !$v.form.login.alpha">Только латиница</p>
      </div>
         <div class="form-group">
         <label for="password">Пароль <span class="text-danger">*</span> </label>
         <input class="form-control" id="password" type="password" 
         v-model.trim="form.password"
         :class="{'is-invalid bg-input-error' : $v.form.password.$error}"
         >
         <p class="error" v-if="$v.form.password.$dirty && !$v.form.password.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.password.$dirty && !$v.form.password.minLength">Введите минимум 6 символов</p>
      </div>


         <div class="form-group">
         <label for="password2">Повторите пароль <span class="text-danger">*</span> </label>
         <input class="form-control" id="password2" type="password" 
         v-model.trim="form.passwordRepeat"
         :class="{'is-invalid bg-input-error' : $v.form.passwordRepeat.$error}"
         >
         <p class="error" v-if="$v.form.passwordRepeat.$dirty && !$v.form.passwordRepeat.required">Обязательное поле</p>
         <p class="error" v-if="$v.form.password.required && $v.form.passwordRepeat.required && !$v.form.passwordRepeat.sameAsPassword">Пароль должен совпадать</p>
      </div>

    <p class="mt-2">
      <small class="text-muted">
        Все поля отмеченные <span class="text-danger">*</span> обязательны для заполнения.
      </small>
    </p>
      <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
   </form>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, email, helpers, sameAs} from 'vuelidate/lib/validators'
const alpha = helpers.regex('alpha', /^[a-zA-Z0-9]*$/)
const alphaRus = helpers.regex('alphaRus', /[А-ЯЁа-яё]/)
import {IMaskDirective} from 'vue-imask';


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
               password: '',
               passwordRepeat: '',
               mask: {
                  mask: '+{7} (000) 000-00-00',
                  lazy: true
               }
            },
            userPhone: '',
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
               ],
         }
      },
      methods: {
         onSubmirForm() {
             this.$v.form.$touch()
         },
         onAccept (e) {
          const maskRef = e.detail;
          this.form.phone = maskRef.value;
         },
         onComplete (e) {
          const maskRef = e.detail;
          this.userPhone = maskRef.unmaskedValue;
        }
      },
      validations: {
         form: {
            name: {
               alphaRus
            },
            fullName: {
               alphaRus
            },
            email: {
               minLength: minLength(4),
               required,
               email
            },
            phone: {
               required
               },
            login: {
               required,
               alpha
            },
            password: {
               minLength: minLength(6),
               required,
            },
            passwordRepeat: {
               required,
               sameAsPassword: sameAs('password')
            },
            profession: {
               maxCount(value) {
                  return value.length <= 3
               }
            }
         }
      },
      directives: {
      imask: IMaskDirective
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
.bg-input-error{
   background-color: rgb(255, 199, 199);
}
</style>