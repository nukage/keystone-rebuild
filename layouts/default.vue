<template>
<div>
  <Header />
 <div class="mainNav__push"></div>
  <NuxtPage/>
 
  <Footer />
</div>
</template>



<script>

  import Header from '~/components/Header.vue'
  import Footer from '~/components/Footer.vue'


export default {
  components: {
    Header, Footer
  }
}
    </script>
