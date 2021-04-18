<template>
                <div class="pag-field">
                <ul class="pagination">
                  <li class="page-item ">
                    <a class="page-link" href="#">&laquo;</a>
                  </li>
                  <li class="page-item " 
                  v-for="page in pages"
                  :key="page"
                  @click="currentPage = page"
                  >
                    <a class="page-link" href="#">{{page}}</a>
                  </li>

                  <li class="page-item">
                    <a class="page-link" href="#">&raquo;</a>
                  </li>
                </ul>
              </div>
</template>

<script>
export default {
    name: 'PagField',
    data(){
        return{
            pages: 5,
            currentPage: 1
        }
    }
}
</script>