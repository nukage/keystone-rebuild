<template>
  <div>
    <NuxtLayout>
      </NuxtLayout>
  </div>
</template>

<script setup>


const route = useRoute()



</script>

<script>
 
export default {
  head() {
    return { 
      link: [ 
        {
          rel: 'stylesheet', href: "https://use.typekit.net/dmo2uqb.css",
      }, 
      ],
      script: [
        {
          src: "https://kit.fontawesome.com/5318d5e5fe.js",
          crossorigin: 'anonymous'
        }
      ]
    }
  }
}

</script>