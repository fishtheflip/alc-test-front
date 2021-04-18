<template>
                <table class="table table-hover" v-if="users.length !== 0">
                <thead>
                <tr>
                    <th scope="col">ФИО</th>
                    <th scope="col">Кол-во</th>
                    <th scope="col">Общая стоимость</th>
                
                </tr>
                </thead>
                <tbody>
                <tr class="table-dark" v-for="(user, index) in users" v-bind:key="index">
                    <th scope="row" 
                    v-bind:class="{active:user.isActive }"
                    @click="changeActive(user)"
                    >{{user.name + ' '}} {{user.surname}}. {{user.middlename}}</th>
                    <td>{{user.items.length}}</td>
                    <td>{{totalSum(user.items)}}</td>
                </tr>
                </tbody>
            </table>
</template>
<script>
export default {
    name: 'TableComp',
    props:['users', 'totalSum', "changeActive"],
    data(){
        return{
            
        }
    }
    
}
</script>