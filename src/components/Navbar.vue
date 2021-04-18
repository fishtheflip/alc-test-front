<template>
            <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
            <div><a class="navbar-brand">{{title}}</a></div>
            <div class="collapse navbar-collapse" id="navbarColor01">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Главная страница
                        <span class="sr-only">(current)</span>
                        </a>
                    </li>
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Добавить Пользователя
                        <span class="sr-only">(current)</span>
                        </a>
                    </li>
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Редактировать Пользователя
                        <span class="sr-only">(current)</span>
                        </a>
                    </li>
                </ul>
            </div>
        </nav>
</template>
<script>

export default {
    name: 'Navbar',
    data(){
        return{
            title: 'Test'
        }
    }
    
}
</script>
