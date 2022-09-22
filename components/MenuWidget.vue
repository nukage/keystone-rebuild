<template>
<li class="menuWidget">
 
<nuxt-link class="menuWidget__link" :to="data[0].acf.link.url">
  <img  class="menuWidget__link__image" v-if="data[0]?.acf?.image" :src="data[0].acf.image"/>
</nuxt-link>
</li>
<!-- 
<div v-html="data[0].content.rendered">

  
</div> -->

 
    
</template>

<script setup>
const props = defineProps({
    slug: String
})

 



const { $wp_uri } = useNuxtApp();
const route = useRoute();

 

const { data, pending, error } = await useAsyncData(props.slug, async () => {
 //   if (process.server){
 
        const data =  await fetch(`${$wp_uri()}/wp-json/wp/v2/menu_widget?slug=${props.slug}`).then(res => res.json());
        return data;
  //  }
})

</script>