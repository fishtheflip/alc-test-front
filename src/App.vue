<template>
  <div id="app">
        <Navbar />
        <div class="container">
          
              <!-- В компонент SortComp передаем функции по сортировки пользователей -->
              <SortComp 
              :filtredByAbc="filtredByAbc"
              :filteredByPrice="filteredByPrice"
              :filtredByTotal="filtredByTotal"
              />
              <!-- В компонент TableComp передаем объект users, -->
              <!-- функции: получения суммы всех элементов, подчеркивание текста,-->
              <!-- изменения видимости модального окна,  -->
              <!-- получения формы редактирования  пользователей -->
              <TableComp  :users="users"
                          :totalSum="totalSum"
                          :changeActive="changeActive"
                          :cangeModalVisible="cangeModalVisible"
                          :setFormControl="setFormControl"
                          
              />

              <!-- Передаем функцию получения формы добавления пользователей -->
              <AddButton :setVisibleForm= "setVisibleForm"/>

              <PagField/>

              <!--Видимость модального окна зависит от свойства modalVisible -->
              <!-- Передаем текущее имя пользователя, id,  -->
              <!-- функции по удалению пользователя, закрыте модального окна -->
              <div v-if="modalVisible">
                    <Modal  :currentModalID="currentModalID"
                            :currentModalName="currentModalName"
                            :closeModal="closeModal"
                            :deleteUser="deleteUser"/>
              </div>

              <!-- Форма редактирования пользователя, передается объект пользователя, -->
              <!-- видимость компонента, обновления пользователя -->
              <div v-if="visibleFormControl">
                    <FormControl  :user="users[currentUserFormControl]"
                                  @updateUser="updateUser"
                                  :setVisibleFormControl="setVisibleFormControl"/>
              </div>
              
              <!-- В компонент передается функция добавления нового пользователя -->
              <div v-if="visibleForm">
                    <Form :setVisibleForm="setVisibleForm" 
                          @addNewUser="addNewUser"/>
              </div>
          
        </div>
    
    
  </div>
</template>

<script>

import Navbar from './components/Navbar'
import SortComp from './components/SortComp'
import TableComp from './components/TableComp'
import AddButton from './components/AddButton'
import PagField from './components/PagField'
import Form from './components/Form'
import dataUser from './data/data'
import Modal from './components/Modal'
import FormControl from './components/FormControl'

// при получении массива входных данных создаем новый объект с добавлением свойства
// isActive для подчеркивания строчки пользователя
const dataVal = Object.assign([], dataUser).map(item=> ({ ...item, isActive: false }))


export default {
  name: 'App',
  components: {
     Navbar, 
     SortComp,
     TableComp,
     AddButton,
     PagField,
     Form,
     Modal,
     FormControl
  },
  data(){
    return{
      users: dataVal,
      hello: 'Hello',
      visibleForm:false,
      modalVisible: false,
      currentModalID: 0,
      currentModalName: '',
      visibleFormControl: false,
      currentUserFormControl: 0
    }
  },
  methods:{

    // видимость формы
      setVisibleForm(){
            if(!this.visibleForm){
              this.visibleForm = true
            } else{
              this.visibleForm = false
            }
    },
    setVisibleFormControl(){
      
            if(!this.visibleFormControl){
              
              this.visibleFormControl = true
            } else{
              this.visibleFormControl = false
            }
    },

    // сумма цены элементов у пользователя 
      totalSum(arr){
            if(arr.length === 1){
                return arr[0].itemCost;
            }
            let calc = 0;
            arr.map((item)=>{
                calc = calc + item.itemCost;
            });
            return calc;
        },

        // функции фильтрации
      filtredByAbc(){
            const filtredArr = this.users.sort(function(a, b){
                let nameA = a.name.toLowerCase(), nameB = b.name.toLowerCase()
                if (nameA < nameB) return - 1;
                if (nameA > nameB)  return 1;
                return 0;
            });
            this.users = filtredArr;
        },
      filtredByTotal(){
            const filtredTotal = this.users.sort(function(a, b){
                let totalA = a.items.length, totalB = b.items.length
                if (totalA < totalB) return - 1;
                if (totalA > totalB)  return 1;
                return 0;
            });
            this.users = filtredTotal;
        },
      filteredByPrice(){
            const totalSum = this.totalSum;
            const filteredByPrice = this.users.sort(function(a, b){
                let totalA = totalSum(a.items), totalB = totalSum(b.items);
                if (totalA < totalB) return - 1;
                if (totalA > totalB)  return 1;
                return 0;
            });
            this.users = filteredByPrice;
        },
        
      // функция выдиления пользователя 
      changeActive(user){
            if(!user.isActive){
                user.isActive = true;
            } else {
                user.isActive = false;
            }
        },
        addNewUser(item){
          dataVal.push({...item, isActive: false, id: dataVal.length});
          console.log(dataVal);
        },
        cangeModalVisible(e, id, name){
            if(!this.modalVisible){
                this.modalVisible = true;
            } else {
                this.modalVisible = false;
            }
          console.log("Deleted",id, name)
          this.currentModalID = id
          this.currentModalName = name
          e.preventDefault()
        },
        closeModal(){
          this.modalVisible = false
        },
        deleteUser(id){
          dataVal.splice(id, 1)
          
          console.log(id)
          this.closeModal()
        },
        setFormControl( item){
          console.log(item)
          this.currentUserFormControl = item.id
          this.setVisibleFormControl()
        },
        updateUser(item){
          dataVal.splice(item.id, 1)
          dataVal.push(item)
        }
  }
}
</script>



