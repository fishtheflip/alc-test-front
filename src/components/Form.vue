<template>
                <form  @submit="addNewUser(e)" method="post">
                <fieldset>
                  <legend>Форма</legend>
                  <div class="form-group">
                    <label for="userName">Фамилия</label>
                    <input type="text" class="form-control" id="userName" aria-describedby="emailHelp" placeholder="Введите фамилию"
                    v-model.trim="nameUser"
                    >
                    
                  </div>
                  <div class="form-group">
                    <label for="userSurname">Имя</label>
                    <input type="text" class="form-control" id="userSurname" placeholder="Введите фамилию"
                    v-model.trim="surnameUser"
                    >
                  </div>
                  <div class="form-group">
                    <label for="userMiddlename">Отчество</label>
                    <input type="text" class="form-control" id="userMiddlename" placeholder="Введите отчество"
                    v-model.trim="middlenameUser">
                  </div>
                    <div class="row">
                      <div class="col">
                        <label for="userMiddlename">Товар</label>
                        <input type="text" class="form-control" placeholder="Товар">
                      </div>
                      <div class="col">
                        <label for="userMiddlename">Стоимость</label>
                        <input type="text" class="form-control" placeholder="Стоимость">
                      </div>
                    </div>
                    <div class="form-btn-field">
                       <button type="submit"  class="btn btn-info">Добавить</button>
                        <button type="reset" @click="setVisibleForm" class="btn btn-danger">Отмена</button>
                    </div>
                 
                </fieldset>
              </form>
</template>
<script>
export default {
    name: 'Form',
    data(){
        return{
            nameUser: '',
            surnameUser: '',
            middlenameUser: '',
            items: 
              {
                itemName:'',
                itemCost: ''
              }

            
        }
    },
    props:['setVisibleForm', "addNewUser"],
    methods:{
  onSubmit(e) {
          this.setVisibleForm()
          let newUser = {
            nameUser: this.nameUser,
            surnameUser: this.surnameUser,
            middlenameUser: this.middlenameUser,
            items: this.items
          }
          console.log(newUser)
          this.nameUser = null
          this.surnameUser = null
          this.middlenameUser = null
          
          e.preventDefault()
}
    }
}
</script>