<template>
   <form class="sign-up">
      <div class="form-group">
         <label for="login">Логин:</label>
         <input class="form-control" id="login" type="text">
      </div>
      <div class="form-group">
         <label for="email">Почта:</label>
         <input class="form-control" id="email" type="text">
      </div>
      <div class="form-group">
         <label for="phone">Телефон:</label>
         <input id="phone" class="form-control" type="text">
      </div>

      <div>
         
      </div>
   </form>
</template>

<script>
   export default {
      
   }
</script>

<style scoped>
.sign-up{
   margin: 50px
}
.form-control{
   width: 400px;
}
.form-group{
   margin-bottom: 15px;
}
label{
   margin-bottom: 5px;
}
</style>