<template>
            <div class="btn-field">
                <button type="button" @click="setVisibleForm" class="btn btn-success">{{buttontext}}</button>
            </div>
</template>
<script>
    export default {
        name: 'AddButton',
        data(){
            return{
                buttontext: 'Добавить'
            }
        }, props:['setVisibleForm']
    }
</script>