<template>
  <div>
    <Login/>
    <Footer/>
  </div>
</template>

<script>
  import Footer from '@/components/Footer.vue'
  import Login from '@/components/LoginForm.vue'

export default {
  components: {
    Login, 
    Footer
  }
}
</script>