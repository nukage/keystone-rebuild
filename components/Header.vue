<template>
<nav   :class="{ 'slim': scrolled }" v-show="handleScroll" class="mainNav">
    <div class="mainNav__inner"> 
      <div class="logo">
        <nuxt-link to="/">
          <img src="~/assets/images/logo.svg" />
    </nuxt-link>
  </div>
  <MenuMain />
  <div class="mainNav__spacer"></div>
  <form class="mainNav__searchForm">
    <label for="search"><img class="searchIcon" src="~/assets/images/magnifying-glass.png"/><span>Enter Keywords Here</span></label>

    <input type="text" id="search" class="search" placeholder="" />
  </form>
  <a class="mainNav__login" href=""><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><defs><clipPath id="t0bba"><path d="M0 0h24v24H0z"/></clipPath></defs><g><g><g><path d="M16.232 12.36C18.142 10.254 18 7 15.923 5.051a5.074 5.074 0 0 0-7.226.312 5.215 5.215 0 0 0 0 6.995 8.623 8.623 0 0 0-4.077 4.385c.38.61.746 1.183 1.223 1.71.548-2.263 2.157-4.136 4.45-4.905 1.374.661 2.97.661 4.343 0a6.887 6.887 0 0 1 4.452 4.91c.477-.525.912-1.098 1.224-1.708a8.623 8.623 0 0 0-4.08-4.392m-.796-1.815a3.428 3.428 0 0 1-1.3 1.316c-.005 0-.01 0-.015.005a3.19 3.19 0 0 1-.713.305c-.044.013-.085.03-.132.042a2.67 2.67 0 0 1-.276.053 3.06 3.06 0 0 1-.487.05h-.097a3.415 3.415 0 0 1-.5-.05c-.085-.015-.176-.031-.263-.053-.045-.012-.085-.029-.132-.042-.247-.075-.521-.17-.712-.305l-.016-.005c-1.641-.933-2.223-3.035-1.3-4.695a3.39 3.39 0 0 1 4.642-1.316c1.642.934 2.224 3.036 1.301 4.695"/></g><g><g/><g clip-path="url(#t0bba)"><path d="M20.67 3.693A12.003 12.003 0 0 0 12 0C5.38 0 0 5.35 0 12c0 3.239 1.33 6.37 3.693 8.634.007.007.01.017.016.023.07.067.145.124.215.188.193.155.386.349.589.514.109.086.222.172.333.25.154.143.384.286.584.391.137.113.277.199.417.285.153.111.37.223.56.325.162.086.327.16.492.238.18.085.357.152.542.248.184.077.369.137.559.204.183.067.345.128.524.183.202.061.41.108.615.159.171.042.337.09.514.124.237.047.476.077.716.11.149.02.293.05.443.064.393.06.789.06 1.188.06.4 0 .795 0 1.187-.06.15-.014.295-.044.443-.064.24-.033.48-.063.717-.11.171-.034.343-.086.514-.124.206-.05.413-.098.615-.159.18-.055.352-.121.524-.183.178-.062.377-.129.56-.204.182-.096.36-.164.54-.248.165-.078.33-.152.493-.238.19-.102.407-.214.56-.325.14-.086.28-.164.416-.285.2-.104.431-.248.585-.39.111-.086.224-.164.333-.25.203-.164.396-.36.589-.515.07-.064.145-.12.215-.188.007-.006.01-.016.016-.023 4.778-4.578 4.941-12.163.363-16.941M12 22.283C6.321 22.283 1.718 17.679 1.718 12c0-2 .564-3.84 1.54-5.413l.002-.005.114-.18.057-.087.065-.096.106-.153c.007-.01.013-.066.02-.066a10.856 10.856 0 0 1 2.6-2.506l.031-.022.165-.108.045-.03c.06-.039.121-.076.182-.114l.028-.017.207-.122.003-.002C11.42.465 17.288 1.684 20.382 6c.047.108.093.175.139.243l.022.033a9.783 9.783 0 0 1 .194.301A10.209 10.209 0 0 1 22.282 12c0 5.68-4.603 10.283-10.282 10.283"/></g></g><g/><g/><g/><g/><g/><g/><g/><g/><g/></g></g></svg> Login</a>
    </div>
</nav>
</template>

<style scoped>
/* .mainNav__nav__submenu {
visibility: hidden;
}
.mainNav__nav__submenu.active{
  visibility: visible;
} */

/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>

<script>
export default{
  name: 'Header',
  data() {
    return { 
      limitPosition: 100,
      scrolled: false,
      lastPosition: 0,
    }
  },
   methods: {
    handleScroll() {
      if (
        this.lastPosition < window.scrollY &&
        this.limitPosition < window.scrollY
      ) {
        this.scrolled = true;
        // move up!
      }

      if (this.lastPosition > window.scrollY) {
        this.scrolled = false;
        // move down
      }

      this.lastPosition = window.scrollY;
      // this.scrolled = window.scrollY > 250;
    },
  },
  beforeMount() {
    window.addEventListener("scroll", this.handleScroll);
    console.log('test')
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  // watch:{
  //   scrolled(){
  //     console.log(this.scrolled);
  //   }
  // }
}
</script>
