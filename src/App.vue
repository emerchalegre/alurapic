<!-- 
  v-on -> Diretiva para setar valor a uma variavel. Igual a @
  v-bind -> Diretiva que recebe o valor de uma variavel. Igual a :

-->

<template>
  <div class="corpo">
    <!--<ul>
      <li v-for="route in routes">
        
          <router-link :to="route.path ? route.path : '/'">{{ route.titulo }}</router-link>

      </li>
    </ul> -->

    <meu-menu :rotas="routes"></meu-menu>
    
  <transition name="pagina">

    <router-view></router-view>
    
  </transition>

  </div>
</template>

<script>

import { routes } from './routes';
import Menu from './components/shared/menu/Menu.vue';

export default {
  components: {
    'meu-menu': Menu
  },

  data() {
    return {
      routes: routes.filter(route => route.menu)
    }
  }  
}
</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }
  
  
.pagina-enter-active,
.pagina-leave-active {
  transition: opacity .3s
}

.pagina-enter,
.pagina-leave-active {
  opacity: 0
}


</style>
