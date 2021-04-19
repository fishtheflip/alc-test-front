<template>
        <div>
                <div class=""  role="dialog">
                <div class="modal-dialog" role="document">
                    <div class="modal-content">

                    <div class="modal-body modal-text">
                        <p>Удалить пользователя: {{currentModalName}} ? </p>
                        
                        
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-primary" @click="deleteUser(currentModalID)">Удалить</button>
                        <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeModal()">Отмена</button>
                    </div>
                    </div>
                </div>
</div>
        </div>
</template>
<script>
export default {
        name: 'Modal',
        props:['currentModalID', 'currentModalName', 'closeModal', 'deleteUser'],
        data(){
        return{
            title: 'Test'
        }
    }
}
</script>