<template>
                <form @submit="onSubmit"  >
                <fieldset>
                  <legend>Форма</legend>
                  <div class="form-group">
                    <label for="userName">Фамилия</label>
                    <input type="text" class="form-control" id="userName" aria-describedby="emailHelp" placeholder="Введите фамилию"
                    v-model.trim="name"
                    >
                    
                  </div>
                  <div class="form-group">
                    <label for="userSurname">Имя</label>
                    <input type="text" class="form-control" id="userSurname" placeholder="Введите фамилию"
                    v-model.trim="surname"
                    >
                  </div>
                  <div class="form-group">
                    <label for="userMiddlename">Отчество</label>
                    <input type="text" class="form-control" id="userMiddlename" placeholder="Введите отчество"
                    v-model.trim="middlename">
                  </div>
                    <div class="row">
                      <div class="col">
                        <label for="userItemName">Товар</label>
                        <input type="text" class="form-control" placeholder="Товар" 
                        v-model.trim="items.itemName">
                      </div>
                      <div class="col">
                        <label for="userItemCost">Стоимость</label>
                        <input type="text" class="form-control" placeholder="Стоимость"
                        v-model.trim="items.itemCost"
                        >
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
            name: '',
            surname: '',
            middlename: '',
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
            name: this.name,
            surname: this.surname,
            middlename: this.middlename,
            items: [this.items]
          }
          
          this.$emit('addNewUser', newUser)
          this.name = null
          this.surname = null
          this.middlename = null
          
          e.preventDefault()
        }
    }
}
</script>