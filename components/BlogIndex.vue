<template>
    <div class="container posts">
        <div class="posts__grid">
            <div>
                <div class="breadcrumb">
                    <Nuxt-link to="/">Home</Nuxt-link> / <Nuxt-link to="/blog">News</Nuxt-link>
                </div>
                <h2>News</h2>
                  <div v-if="data && (!route.params.pageNum || route.params.pageNum == 1)" class="newsCardBig">
                    <Nuxt-link :to="`/blog/${data[0].slug}`" class="newsCardBig__thumb">
                        <img  v-if="data[0].featured_image?.blogLg" :src="data[0].featured_image.blogLg" />
                        <img   v-else src="http://placehold.jp/865x466.png"/>     
                    </Nuxt-link>
                    <div class="newsCardBig__content">
                        <nuxt-link :to="`/blog/${data[0].slug}`" >
                            <h3 class="newsCardBig__title" v-html="data[0].title"></h3>
                        </nuxt-link>
                        <div class="newsCardBig__date" v-html="data[0].date"></div>
                        <div class="newsCardBig__excerpt" v-html="data[0].excerpt">
                        </div>
                    </div>
                </div>
                <div class="newsCardsSmall">
                    <div class="newsCardSmall" v-for="post in getPosts(data)" :key="post.id">
                        <nuxt-link :to="`/blog/${post.slug}`" class="newsCardSmall__thumb">
                            <img v-if="post.featured_image?.blogSm" :src="post.featured_image.blogSm" />
                            <img v-else src="http://placehold.jp/422x393.png" />
                        </nuxt-link>
                            <div class="newsCardSmall__content">
                                <nuxt-link :to="`/blog/${post.slug}`" class="newsCardSmall__title">{{post.title}}</nuxt-link>
                            <nuxt-link :to="`/blog/${post.slug}`" class="newsCardSmall__date">{{post.date}}</nuxt-link>
                            <div class="newsCardSmall__excerpt">
                                <p v-html="post.excerpt">
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                <ul class="posts__grid__pagi">
                    <li v-if="Number(route.params.pageNum) > 1">
                        <nuxt-link :to="`/blog/page/${pageNum() - 1}`"><i class="fa-solid fa-angle-left"></i></nuxt-link>
                    </li>
                        <li v-for="n in getNumberOfPages()" :key="n">
                            <nuxt-link v-if="isCurrentPage(n)" :to="`/blog/page/${n}`">{{n}}</nuxt-link>
                            <template v-else>{{n}}</template>
                        </li> 
                    <nuxt-link :to="`/blog/page/${pageNum() + 1}`" v-if="getNumberOfPages() != route.params.pageNum "><i class="fa-solid fa-angle-right"></i></nuxt-link>
                </ul>
            </div>
            <PostsSidebar />
        </div>
    </div>
</template>
<script setup>
const perPage = 4;
function getNumberOfPages(){
    return Math.floor(data.value.length / perPage);
}
function isCurrentPage(n){
    if (n  == route.params.pageNum ){
        return false;
    } else if (!route.params.pageNum && n == 1){
        return false;
        }
    else{
        return true;
    }
}
function pageNum(){
    if (!route.params.pageNum){
        return 1;
        } else {
        return Number(route.params.pageNum);
    }
}
const { $wp_uri, $formatDate } = useNuxtApp();
const route = useRoute();
const uid = 'postsIndex';
// function makePostLink(link){
//     return '/blog/' + link;
// } 
const { data, pending, error } = await useAsyncData(uid, async () => {
//    if (process.server){
        return await fetch(`${$wp_uri()}/wp-json/qntm/v1/posts`).then(res => res.json());
//    }
})


function getPosts(dataset){
    if (!route.params.pageNum || route.params.pageNum == 1) {
        return dataset.slice(1, (perPage + 1));
    }
    else {
        return dataset.slice(((route.params.pageNum * perPage) - perPage + 1), (route.params.pageNum * perPage + 1));
    }
}  
 
</script>