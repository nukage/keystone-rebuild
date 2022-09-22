<template>
<div  class="mainNav__wrapper">
<div v-if="data">
 
<div class="mainNav__nav">
    <template v-for="item in data" :key="item['ID']"> 
    <div class="mainNav__nav__item"  v-if="item.menu_item_parent == '0'">
        <nuxt-link class="mainNav__nav__item__textLink" v-if="item.classes[0] =='hasChildren'"  @click="eventMenuL1(item['ID'])" :class="item['ID'] == menuL1 ? 'open' : 'closed'">
        {{item.title}}
 
        </nuxt-link>
        <nuxt-link  class="mainNav__nav__item__textLink" v-else :to="item.url">{{item.title}}</nuxt-link> 
        

        <!-- <Transition> -->
            <div class="mainNav__nav__submenu"   v-if="item['ID'] == menuL1">
            <template  v-for="itemL2 in data" :key="itemL2['ID']">
            
                <template v-if="itemL2['menu_item_parent'] == item['ID']">
                <a @click="clickEventMenuL2(itemL2['ID'])" @mouseover="eventMenuL2(itemL2['ID'])" :class="itemL2['ID'] == menuL2 ? 'open' : 'closed'">
                {{ itemL2.title }} 
                </a>
                <transition name="slide">
                    <div class="mainNav__nav__submenu__l2__wrapper" v-show="itemL2['ID'] == menuL2">
                <ul class="mainNav__nav__submenu__l2">
                    <template v-for="itemL3 in data" :key="itemL3['ID']">
               
                    <template v-if="itemL3['menu_item_parent'] == itemL2['ID'] && itemL3.url == '#widget'">
                    <MenuWidget :slug="itemL3.classes[0]" />
                    </template>
                <li :class="itemL3.classes.toString(' ')" v-else-if="itemL3['menu_item_parent'] == itemL2['ID']">
                <nuxt-link class="mainNav__nav__submenu__l2__link" @click="clickEventMenuItem()" :href="nuxtLinkMaker(itemL3.url)"> 
                {{ itemL3.title }}
                </nuxt-link>
                <template v-for="itemL4 in data" :key="itemL4['ID']">
                    <div class="mainNav__nav__submenu__l3" v-if="itemL4['menu_item_parent'] == itemL3['ID']">
                    <Nuxt-Link @click="clickEventMenuItem()" :to="nuxtLinkMaker(itemL4.url)">
                    {{ itemL4.title }}
                
                    </Nuxt-Link>
                    </div>
                </template>
                </li>
                </template>
                <Nuxt-link :to="itemL2.url" class="mainNav__nav__viewAllLink" v-if="item.title == 'Products'">VIEW ALL PRODUCTS</Nuxt-link>
                </ul>
                </div>
                </transition>
                </template>
            </template>
               
        </div>
         <a @click="eventMenuL1(item['ID'])"  class="plusMinus" v-if="item.title == 'Products' || item.title == 'More'"><span v-if="item['ID'] == menuL1">-</span><span v-else>+</span></a>
        <!-- </Transition> -->

    </div>
</template>
 
</div>
</div>
</div>
 
  <div @click="menuL2 = 0" @mouseover="menuL2 = 0" v-if="menuL2" class="mainNav__overlay"></div>
 
</template>








<script setup>

const { $wp_uri, $scrollFix  } = useNuxtApp();
const route = useRoute();

 

let menuL1 = ref(0);
let menuL2 = ref(0);

watch(() => route.fullPath,() => {
    menuL1.value = 0;
    menuL2.value = 0;
    $scrollFix(route.hash);
    }
)

 
function nuxtLinkMaker(url){
    const arr = url.split('#') 

    if (arr[1]){
        return {
            path: arr[0],
            hash: "#" + arr[1]
        }
    }else {
        return {
            path: url,
        }
    }
}



function eventMenuL1(itemID) {
    if (menuL1.value == itemID) {
        menuL1.value = 0;
        menuL2.value = 0;
    } else {
        menuL2.value = 0;
        menuL1.value = itemID;
    }
}

function eventMenuL2(itemID) {
    menuL2.value = itemID;
}
function clickEventMenuL2(itemID){
    if (menuL2.value == itemID) {
        menuL2.value = 0;
    } else {
        menuL2.value = itemID;
    }
}

function clickEventMenuItem(itemID){
        menuL2.value = 0;
}


// const props = defineProps({
//     data: Object
// })
 

//  onMounted(()=>{
//     console.log('onMounted ' + route.fullPath)
//     // scrollFix();
// })

const { data, pending, error } = await useAsyncData("menu", async () => {
 //   if (process.server){
        const menus =  await fetch(`${$wp_uri()}/wp-json/menus/v1/menus`).then(res => res.json());
        const menu = menus.find((r)=>r.slug === 'menu-1');
        const menuChildren =  await fetch(`${$wp_uri()}/wp-json/menus/v1/menus/${menu.term_id}`).then(res => res.json());
        return menuChildren;
  //  }
})


</script>


<style scoped>
.v-enter-active,
.v-leave-active {
  transition: width 0.3s ease;
  width: 100%;
   overflow:hidden;
   height:30px;
   white-space: nowrap;
}

.v-enter-from,
.v-leave-to {
  width:0%;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.2s ease;
  opacity: 100%;
   overflow:hidden;
 
}

.slide-enter-from,
.slide-leave-to {
  opacity:0%;
}
</style>