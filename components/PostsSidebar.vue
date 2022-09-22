<template>

            <div class="postsSidebar">

          
                <div class="postsSidebar__forms">
                    <h3>
                        Sign up for updates 
                    </h3>
                        <form>
                            <label><img src="~/assets/images/icons/envelope-blk.png"/>Enter Email</label>
                            <input name="email" type="text" />
                        </form>
                    <h3>
                        Search News
                    </h3>
                        <form>
                            <label><img src="~/assets/images/icons/search-blk.png"/>Enter Keywords</label>
                            <input name="email" type="text" />
                        </form>
                </div> 
                    <div v-if="data" class="postsSidebar__featuredPosts">
                   
                        <h3 class="postsSidebar__featuredPosts__heading underlines">
                            Featured Posts
                        </h3> 
                        <div class="postsSidebar__featuredPosts__postsLink" v-for="post in data" :key="post.id">
                            <Nuxt-Link :to="`/blog/${post.slug}`" class="postsSidebar__featuredPosts__postTitle">
                                {{ post.title.rendered }}
                            </Nuxt-Link>
                            <nuxt-link  :to="`/blog/${post.slug}`" class="postsSidebar__featuredPosts__postDate">
                                {{ $formatDate(post.date)  }}
                            </nuxt-link>
                        </div>

                    </div>
      
                    <div v-if="social.data.value.acf.qntm_social_links" class="postsSidebar__followUs">
                        <h3 class="underlines">
                            Follow Us
                        </h3>
                        <div  class="postsSidebar__followUs__links">

                            <nuxt-link target="_blank" :to="link.social_media_link" class="postsSidebar__followUs__links__link" v-for="(link, n) in social.data.value.acf.qntm_social_links" :key="n">
                    
                           <i :class="`fab fa-${link.icon}`" aria-hidden="true"></i>
                        </nuxt-link>
                        </div>
 
                    </div>

            </div>
            
            </template>

            <script setup>

const { $wp_uri, $formatDate } = useNuxtApp();
const route = useRoute();

const uid = 'postsSidebar';

 

// function makePostLink(link){
//     return '/blog/' + link;
// } 

const social = await useAsyncData('social', async () => { 
    return await fetch(`${$wp_uri()}/wp-json/acf/v3/options/acf-social-media`).then(res => res.json());
})
const { data, pending, error } = await useAsyncData(uid, async () => {
//    if (process.server){
        return await fetch(`${$wp_uri()}/wp-json/wp/v2/posts?page=1&per_page=4&_embed=1`).then(res => res.json());
//    }
})
 

</script>