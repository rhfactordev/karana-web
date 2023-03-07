<template>
  <main>
    <section class="container">
      <div class="text-center">
        Karana
      </div>
    </section>

    <section class="container bg-light py-5">
      <div class="row">
        <div class="col-12 col-sm-12 col-md-6 p-md-5">
          <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/zpOULjyy-n8?rel=0" allowfullscreen />
          </div>
        </div>
        <div class="col-12 col-sm-12 col-md-6 p-5">
          <h1 class="py-3">
            O poder do autoconhecimento na palma da mão
          </h1>
          <p>Preencha os dados abaixo para acessar seu mapa astral e obter detalhes importantes para alcançar todo o potencial da sua vida.</p>
          <form>
            <div class="form-group">
              <label for="exampleInputEmail1">Email address</label>
              <input id="exampleInputEmail1" type="email" class="form-control" aria-describedby="emailHelp">
            </div>
            <button type="submit" @click.stop.prevent="submit()" class="btn btn-primary btn-lg btn-block">
              Obter o conhecimenot!
            </button>
          </form>
        </div>
      </div>
    </section>

    <section class="container bg-primary py-5">

      <div class="text-center mb-5">
        <h2>Entenda o seu mapa astral</h2>
        <p class="w-md-50 m-auto">
          Conheça os benefícios de obter o seu mapa astral This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.
        </p>
      </div>

      <div class="card-deck">
        <div class="card border-light">
          <img src="https://images.unsplash.com/photo-1511945863317-d60e146e9016?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTM0fHx3b21hbnxlbnwwfDB8MHx8&auto=format&fit=crop&w=800&q=60" class="card-img-top" alt="Imagem 1">
          <div class="card-body">
            <h5 class="card-title">
              Card title
            </h5>
            <p class="card-text">
              This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.
            </p>
            <p class="card-text">
              <small class="text-muted">Last updated 3 mins ago</small>
            </p>
          </div>
        </div>
        <div class="card border-light">
          <img src="https://images.unsplash.com/photo-1507835661088-ac1e84fe645f?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NHx8ZnJlZWRvbSUyMGdpcmx8ZW58MHx8MHx8&auto=format&fit=crop&w=800&q=60" class="card-img-top" alt="Imagem 2">
          <div class="card-body">
            <h5 class="card-title">
              Card title
            </h5>
            <p class="card-text">
              This card has supporting text below as a natural lead-in to additional content.
            </p>
            <p class="card-text">
              <small class="text-muted">Last updated 3 mins ago</small>
            </p>
          </div>
        </div>
        <div class="card border-light">
          <img src="https://images.unsplash.com/photo-1542353436-312f0e1f67ff?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTB8fGZyZWVkb20lMjBnaXJsfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=800&q=60" class="card-img-top" alt="Imagem 2">
          <div class="card-body">
            <h5 class="card-title">
              Card title
            </h5>
            <p class="card-text">
              This is a wider card with supporting text below as a natural lead-in to additional content. This card has even longer content than the first to show that equal height action.
            </p>
            <p class="card-text">
              <small class="text-muted">Last updated 3 mins ago</small>
            </p>
          </div>
        </div>
      </div>
    </section>

    <section class="container bg-light">
      <div class="row">
        <div class="d-none d-md-table-cell col-md-6 bg-1">
        </div>
        <div class="col-md-6 p-5">
            <h1 class="mt-5 mb-3">Only the finest,<br/>locally sourced produce.</h1>
            <p>All fresh ingredients in our dishes are sourced from local farms and farmer's markets. Making use of only fresh, seasonally available produce infuses the dishes we prepare with a unique authenticity.</p>
            <form class="my-5">
              <div class="form-group">
                <label for="exampleInputEmail1">Email address</label>
                <input id="exampleInputEmail1" type="email" class="form-control" aria-describedby="emailHelp">
              </div>
              <button type="submit" @click.stop.prevent="submit()" class="btn btn-primary btn-lg btn-block">
                Obter o conhecimenot!
              </button>
            </form>
        </div>
      </div>
    </section>

  </main>
</template>

<style scoped>
  .bg-1{
    background-image: url('https://images.unsplash.com/photo-1664575601786-b00156752b61?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NXx8d29tYW58ZW58MHwxfDB8fA%3D%3D&auto=format&fit=crop&w=800&q=60');
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    height: 600px!important;
  }
</style>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  methods: {
    submit(){
      this.$router.push('/checkout');
    }
  }
})
</script>
