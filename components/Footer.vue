<template>    
<footer>

  <div v-if="data" class="container">
    <div class="footerTop">
      <div class="footerTop__colOne">
        <h3>Have a question?</h3>
        <div class="footerTop__colOne__iconlinks">
          <a class="" :href="`mailto:${data.acf.contact_email}`">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
              <!--! Font Awesome Free 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free (Icons: CC BY 4.0, Fonts: SIL OFL 1.1, Code: MIT License) Copyright 2022 Fonticons, Inc. --><path d="M0 128C0 92.65 28.65 64 64 64H448C483.3 64 512 92.65 512 128V384C512 419.3 483.3 448 448 448H64C28.65 448 0 419.3 0 384V128zM48 128V150.1L220.5 291.7C241.1 308.7 270.9 308.7 291.5 291.7L464 150.1V127.1C464 119.2 456.8 111.1 448 111.1H64C55.16 111.1 48 119.2 48 127.1L48 128zM48 212.2V384C48 392.8 55.16 400 64 400H448C456.8 400 464 392.8 464 384V212.2L322 328.8C283.6 360.3 228.4 360.3 189.1 328.8L48 212.2z"/></svg>{{data.acf.contact_email}}</a>
          <a class="footerTop__colOne__iconlink" :href="`tel:${data.acf.contact_phone}`"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Free 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free (Icons: CC BY 4.0, Fonts: SIL OFL 1.1, Code: MIT License) Copyright 2022 Fonticons, Inc. --><path d="M511.2 387l-23.25 100.8c-3.266 14.25-15.79 24.22-30.46 24.22C205.2 512 0 306.8 0 54.5c0-14.66 9.969-27.2 24.22-30.45l100.8-23.25C139.7-2.602 154.7 5.018 160.8 18.92l46.52 108.5c5.438 12.78 1.77 27.67-8.98 36.45L144.5 207.1c33.98 69.22 90.26 125.5 159.5 159.5l44.08-53.8c8.688-10.78 23.69-14.51 36.47-8.975l108.5 46.51C506.1 357.2 514.6 372.4 511.2 387z"/></svg>{{ data.acf.contact_phone }}</a>
        </div>
        <div class="footerTop__follow"><h4>Follow: 
 

                                      <nuxt-link target="_blank" :to="link.social_media_link" class="postsSidebar__followUs__links__link" v-for="(link, n) in social.data.value.acf.qntm_social_links" :key="n">
                    
                           <i :class="`fab fa-${link.icon}`" aria-hidden="true"></i>
                        </nuxt-link>


          </h4></div> 
      </div> 
    
      <div class="footerTop__colTwo">
        <div v-if="acfFooter.data.value.acf.portal_info" v-html="acfFooter.data.value.acf.portal_info"></div>
<RouterLink :target="acfFooter.data.value.acf.portal_info_link.target" :href="acfFooter.data.value.acf.portal_info_link.url" class="footerTop__colTwo__btn">{{acfFooter.data.value.acf.portal_info_link.title}}</RouterLink>
      </div>
    </div>
    <div class="footerBottom">
      <div class="footerBottom__grid">
        <div>
       
          <img class="footerBottom__logo" :src="acfFooter.data.value.acf.footer_logo"/>
 

        <div v-if="data.acf.address" v-html="fixLineBreaks(data.acf.address)"></div> 
        </div>
       <MenuFooter/>
      </div>
    </div>
  </div>
</footer>
</template>

<script setup>
 

const { $wp_uri } = useNuxtApp();
const uid = 'footer';
const { data, pending, error } = await useAsyncData('uid' + '-options', async () => { 
    return await fetch(`${$wp_uri()}/wp-json/acf/v3/options/options`).then(res => res.json());
})

const acfFooter = await useAsyncData(uid + '-footer', async () => { 
    return await fetch(`${$wp_uri()}/wp-json/acf/v3/options/acf-footer`).then(res => res.json());
})


const social = await useAsyncData(uid + '-social', async () => { 
    return await fetch(`${$wp_uri()}/wp-json/acf/v3/options/acf-social-media`).then(res => res.json());
})

function fixLineBreaks(str){
  if (typeof(str) !== 'string'){
    return;
  }  else {
        return str.replace(/\r\n/g, "<br>");
  }
}
</script>