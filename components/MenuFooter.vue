<template>

 
<template v-if="data">
<template v-for="item in data" :key="item['ID']"> 
<div  v-if="item.menu_item_parent == '0'">
    <h3><nuxt-link :to="item.url">{{item.title}}</nuxt-link></h3>
        <template v-for="itemL2 in data" :key="itemL2['ID']">
        <nuxt-link :to="itemL2.url" v-if="itemL2['menu_item_parent'] == item['ID']">{{itemL2.title}}</nuxt-link>
    </template>
</div>
 </template>
</template>
</template>

<script setup>
const { $wp_uri, $scrollFix  } = useNuxtApp();
const { data, pending, error } = await useAsyncData("footerMenu", async () => {
 //   if (process.server){
        const menus =  await fetch(`${$wp_uri()}/wp-json/menus/v1/menus`).then(res => res.json());
        const menu = menus.find((r)=>r.slug === 'footer-main-menu');
        const menuChildren =  await fetch(`${$wp_uri()}/wp-json/menus/v1/menus/${menu.term_id}`).then(res => res.json());
        return menuChildren;
  //  }
})
</script>