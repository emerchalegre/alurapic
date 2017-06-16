<template>
    <div>
        
        <ul>
            <li v-for="route in rotas">
                <router-link :to="route.path ? route.path : '/'">{{ route.titulo }}</router-link>
            </li>
        </ul>

    </div>
</template>
<script>
export default {
  props: {
      rotas: {
          required: true,
          type: Array
      }
  }
}
</script>
<style>

</style>
