<template>

<div>
    products: {{products.length}} <br/>
    categories: {{categories}}<br/>
    l2products: {{l2products?.length}}

    

 

</div>

</template>


<script>
// import { arrayBuffer } from 'stream/consumers';

 

export default{
    props:['products'],
    data() {
        categories: []
        index: []
    },
    watch:{
        products(){
            if (this.products[0]){
                // this.setIndex();
 
            }
        }
    },
    methods: {
        heirachy(){
         
            let map = state.products.filter(product => product[className].toLowerCase() === category.toLowerCase());
        },

        getCategories(key, input){
            if (typeof(input) !== 'object') {
                return;
            } else {

                
                let list = input.map(e => {
                    return e[key];
            })
            list = [...new Set(list)];
            return list;
                }
        },

        setIndex(){
            let level2 = this.getCategories('Item_Class2', this.products);
            // let arr = this.index;
            let arr = [];
            level2.forEach(l2item => {
                const l2products = this.products.filter(product => product.Item_Class2 === l2item);
                const l3items =  this.getCategories('Item_Class3', l2products).map(l3category => {
                const l3products = l2products.filter(product => product.Item_Class3 === l3category);
                    return {
                        name: l3category, 
                        ids: l3products.map(product => {return product.item_id}),
                        children: this.getCategories('Item_Class4', l3products).map(l4category => {
                            const l4products = l3products.filter(product => product.Item_Class4 === l4category);
                            return {
                                name: l4category,
                                ids: l4products.map(product => {return product.item_id}),
                            }
                        })
                    }
                    });
                arr.push(
                    {
                        "name" : l2item, "ids": l2products.map(product => {return product.item_id}), "children": l3items
                    }
                )
            })
            this.index  = arr;
            console.log('here is the category index: ')
            console.log(this.index);
        },

        getSubLevelCategories () {
            return x;
        let level_2 = this.products.map(product => {return product.Item_Class2} );
        level_2 = [...new Set(level_2)];
        this.categories = level_2;
        let l2products = [];
        level_2.forEach(category => {
            let products = this.products.filter(product => category === product.Item_Class2);
            l2products.push(products);
        })
        this.l2products = l2products;




        return level_2;
     },
    }
}
</script>