<template>
                    <form  @submit="onSubmit">
                <fieldset>
                  <legend>Форма Редактирования</legend>
                  <div class="form-group">
                    <label for="userName"></label>
                    <input type="text" class="form-control" id="userName" aria-describedby="emailHelp"  
                    v-model.trim="nameUser"
                    
                    >
                    
                  </div>
                  <div class="form-group">
                    <label for="userSurname"></label>
                    <input type="text" class="form-control" id="userSurname" 
                    v-model.trim="surnameUser"
                    
                    >
                  </div>
                  <div class="form-group">
                    <label for="userMiddlename"></label>
                    <input type="text" class="form-control" id="userMiddlename"
                    v-model.trim="middlenameUser"
                    
                    >
                  </div>
                    <div class="row" v-for="(item, index) in items" v-bind:key="index">
                      
                      <div class="col">
                        <label for="userCostItem" ></label>
                        <input type="text" class="form-control"  
                        v-model.trim="item.itemName"
                        >
                        
                      </div>
                      <div class="col">
                        <label for="userCostItem"></label>
                        <input type="text" class="form-control" 
                        v-model.trim="item.itemCost"
                        >

                      </div>
                    </div>

                    <div class="total-sum">
                      <div class="toast show " role="alert" aria-live="assertive" aria-atomic="true">
                        <div class="toast-body ">
                          <span>Итог: {{totalSum()}}</span>
                        </div>
                      </div>
                    </div>


                    <div class="form-btn-field">
                       <button type="submit"  class="btn btn-info"> Добавить</button>
                        <button type="reset"  class="btn btn-danger" @click="setVisibleFormControl">Отмена</button>
                    </div>





                </fieldset>
              </form>
</template>
<script>
export default {
    name:'FormControl',
    props:['user', 'updateUser', 'setVisibleFormControl'],
    data(){
      return{
        nameUser: this.user.name,
        surnameUser: this.user.surname,
        middlenameUser: this.user.middlename,
        items: this.user.items
      }
    },
    methods:{
      totalSum(){
        let sum = 0;
        this.items.map((item)=> sum = sum + item.itemCost)
        return sum
      },
      onSubmit(e) {
          
          let newUser = {
            id: this.user.id,
            name: this.nameUser,
            surname: this.surnameUser,
            middlename: this.middlenameUser,
            items: this.items
            
          }
          
          this.$emit('updateUser', newUser)

          
          
          e.preventDefault()
        }
    }

}
</script>