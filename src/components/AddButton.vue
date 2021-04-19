<template>
        <div class="btn-field">
            <button type="button" @click="setVisibleForm" class="btn btn-success">Добавить</button>
        </div>
</template>
<script>
    export default {
        name: 'AddButton',
        props:['setVisibleForm']
    }
</script>