        <template>            
        <div v-if="title" class="interiorTitle">
            <div class="container">
                <h1 v-html="title"></h1>
                <p v-if="subhead" v-html="subhead">
                </p>
  
            </div>
        </div>
        </template>

        <script>
        export default{
            props:['title','subhead']
        }
        </script>