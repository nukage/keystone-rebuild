<template>
    <div class="breadcrumb mt-var">
        <Nuxt-link to="/">Home</Nuxt-link> / 
        <div class="inline" v-if="l1 === 'Products'">
            Products
            <div  class="inline" v-if="l2"> / <Nuxt-link v-if="l3" :to="'/products/'+ $makeSlug(l2)">{{l2}}</Nuxt-link> <div class="inline" v-else>{{l2}}</div> </div>
            <div class="inline" v-if="l3"> / <Nuxt-link v-if="l4" :to="'/products/'+$makeSlug(l2)+'#'+ $makeSlug(l3)">{{l3}}</Nuxt-link><div class="inline" v-else>{{l3}}</div></div>
            <div class="inline" v-if="l4"> / <Nuxt-link v-if="l5" :to="'/products/'+$makeSlug(l2)+'#'+ $makeSlug(l3) + '_' +$makeSlug(l4)">{{l4}}</Nuxt-link><div class="inline" v-else>{{l3}}</div></div>
            <div class="inline" v-if="l5"> / <div class="inline">{{l5}}</div></div>
        </div>
        <div class="inline" v-else-if="l1 === 'Case Studies' && title">
        <Nuxt-link  to="/case-studies/">Case Studies</Nuxt-link>  <span v-if="title"> / {{title}}</span>
        </div>
        <div class="inline" v-else>
            
            <!-- 'Not products..' -->
            <span v-if="l1">{{l1}}</span> 
             
            <span v-if="l2"> / {{l2}}</span> 
            <span v-else-if="post_type == case_study && title">{{title}}</span>
            <span v-if="l3"> / {{l3}}</span>
            <span v-if="l4"> / {{l4}}</span>
        </div>
</div> 
</template>
<script>
export default{
    props:['l1', 'l2', 'l3', 'l4', 'l5', 'post_type','title']
}
</script>