<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <SortComp 
      :filtredByAbc="filtredByAbc"
      :filteredByPrice="filteredByPrice"
      :filtredByTotal="filtredByTotal"
      />
      <TableComp :users="users"
      :totalSum="totalSum"
      :changeActive="changeActive"/>
      <AddButton :setVisibleForm= "setVisibleForm"/>
      <PagField/>
      
      <div v-if="visibleForm === true">
        <Form :setVisibleForm="setVisibleForm" :addNewUser="addNewUser"/>
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


export default {
  name: 'App',
  components: {
     Navbar, 
     SortComp,
     TableComp,
     AddButton,
     PagField,
     Form
  },
  data(){
    return{
      users: dataUser,
      hello: 'Hello',
      visibleForm:false
    }
  },
  methods:{
      setVisibleForm(){
            if(this.visibleForm === false){
              this.visibleForm = true
            } else{
              this.visibleForm = false
            }
    },
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
      
      filtredByAbc(){
            const filtredArr = this.users.sort(function(a, b){
                let nameA=a.name.toLowerCase(), nameB = b.name.toLowerCase()
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
      changeActive(user){
            if(user.isActive === false){
                user.isActive = true;
            } else {
                user.isActive = false;
            }
        },
        addNewUser(){

          

        }
      
  }
}
</script>



