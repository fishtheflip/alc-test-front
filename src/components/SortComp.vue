<template>
            <div class="main-block">
                <div>
                    <span>Сортировка:</span>
                </div>
                <div class="btn-group" role="group" aria-label="Basic example">
                    <button type="button" class="btn btn-secondary" @click="filtredByAbc()" >По алфавиту</button>
                    <button type="button" class="btn btn-secondary" @click="filteredByPrice()" >По стоимости</button>
                    <button type="button" class="btn btn-secondary" @click="filtredByTotal()" >По кол-во</button>
                </div>
            </div>
</template>

<script>


export default {
    name: 'SortComp',
    props:["filtredByAbc", "filteredByPrice", "filtredByTotal"]
}
</script>
