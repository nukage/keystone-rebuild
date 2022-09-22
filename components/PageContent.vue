<template>
<div>
  


   <v-runtime-template :template="content"></v-runtime-template>
   <!-- <div v-html="content"></div> -->
</div>
</template>

<script>
import VRuntimeTemplate from "vue3-runtime-template";
import RouterLink from "~/components/RouterLink";
import Breadcrumb from "~/components/Breadcrumb"


export default{
components: {
    RouterLink,
    VRuntimeTemplate,
    Breadcrumb
  },
    setup(){
        const { $tinySliderz, $waitForElement, $glightbox, $tabs, $statements } = useNuxtApp();
    },
    data(){
        return {
            tabsOptions:{
                element: '.tabGroup',
                params: {
                    elem: 'tabs'
                }
            },
            sliderOptions: {
                single: {
                    element: '.slider-block__single',
                    wrapper: '.slider-block__wrapper',
                        params: {
                        'items': 1,
                        'slideBy': 'page',
                        'autoplay': false,
                        "mouseDrag": true,
                        }
                    },
                multi: {
                    element: '.slider-block__multi',
                    wrapper: '.slider-block__wrapper',
                        params: {
                            'items': 3,
                            'slideBy': 1,
                            'autoplay': false,
                            "mouseDrag": true,
                        }
                    }
                },
                lightboxOptions:{
                    element: '.glightbox',
                    params:{

                    }
                },
                lightboxOptions2:{
                    type: 'custom',
                    element: '.lightbox__iconImage',
                    params:{

                    }
                }
            }
    },
    props:['content'],
    methods: { 
        getSlider(){
            const single = /slider-block__single/;
            const multi = /slider-block__multi/;
            const lightbox = /glightbox/;
            const tabs = /tabGroup/;
            const homeAbout = /homeAbout/;
            const lightbox2 = /lightbox/;

            if (single.test(this.content)) {
                this.$waitForElement('.slider-block__single', 3000).then(()=>  {
                    console.log('single slider block has loaded');
                    this.$tinySliderz(this.sliderOptions.single);
                }).catch((err)=>{
                    console.log(err)
                })
            } 
            if (multi.test(this.content))  {
                this.$waitForElement('.slider-block__multi', 3000).then(()=>  {
                    console.log('multi slider block has loaded');
                    this.$tinySliderz(this.sliderOptions.multi);
                }).catch((err)=>{
                    console.log(err)
                })
    
            } 
            if (lightbox.test(this.content)){
                this.$waitForElement(this.lightboxOptions.element, 3000).then(()=>{
                     console.log('Lightbox has loaded');
                     this.$glightbox(this.lightboxOptions);
                }).catch((err)=>{
                    console.log(err)
                })
            }
            if (tabs.test(this.content)){
                this.$waitForElement(this.tabsOptions.element, 3000).then(() => {
                    console.log('tabs have loaded');
                    this.$tabs(this.tabsOptions);
                }).catch((err)=>{
                    console.log(err)
                })
            }
            if (homeAbout.test(this.content)) {
                this.$waitForElement('.homeAbout', 3000).then(()=>  {
                    console.log('Home About');
                    this.$statements();
                }).catch((err)=>{
                    console.log(err)
                })
            } 
            if (lightbox2.test(this.content)) {
                this.$waitForElement('.lightbox', 3000).then(()=>  {
                    console.log('Home About');
                    this.$glightbox(this.lightboxOptions2);
                }).catch((err)=>{
                    console.log(err)
                })
            } 
            // else {
            //     console.log('There is no slider on this page');
            // }

            // console.log('queryForSlider');
            // const testStr = /slider-block/;
            // if (testStr.test(this.content)){
            //     console.log(testStr.test(this.content))
            //     if(document.querySelector('.slider-block')){
            //         this.$tinySliderz(this.sliderParams);
            //     } else {
  
            //         while (document.querySelector('.slider-block') === false){
            //             setTimeout(() =>{
            //                 if (document.querySelector('.slider-block') === true){
            //                     console.log('test');
            //                     this.$tinySliderz(this.sliderParams);
            //                 }
            //             },10)
            //         }
            //          this.$tinySliderz(this.sliderParams);
            //     }
            // };  
        }
    },
    mounted(){
        this.getSlider();
 
        // setTimeout(() =>{
        //     this.tinySlider();
        // },0)
        // console.log(this.queryForSlider());
    },
    updated(){
        this.getSlider();
        // setTimeout(() =>{
        //     this.tinySlider();
        // },0)  
    }
}
</script>