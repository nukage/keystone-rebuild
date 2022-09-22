<template>


<Nuxt-link :title="title" :to="href"><slot></slot></Nuxt-link>

</template>

        <script>
        export default{
            props:['title','href']
        }
        </script>