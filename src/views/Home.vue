<template>
    <div>
        <div class="header">
            <img id="image"  src="../assets/306321046_1990929511112000_6792836128897096191_n.jpg" >
        </div>
        <div class="body">
            <h2 id="h2" >Latest Mobile Phones Prices</h2>
            <div style="width: 50%; height: 5rem;">
                <div class="card" >
                    <div class="card-body">
                        <h5 class="card-title" id="h2">Mobile Mania -M.A Jinnah Road</h5>
                    </div>
                </div>
            </div>

            <div style="width: 50%; height: 5rem; margin-top: 20px;">
                <div>
                    
                </div>
                <table class="table table-bordered" v-for="items in categories">
                        <h2 scope="col" >{{items.category_name}}</h2>

                    <tbody v-for="items in products">
                        <tr>
                            <td>
                                <span>
                                    <h6 style="color:blue">{{items.product_name}}</h6>
                                    <br>
                                    <p style="color:gray; font-weight: 800; ">
                                        Market Price:Rs.{{items.product_market_price}}
                                    </p>
                                    <br>
                                    <h7>
                                        Discounted Price:Rs.{{items.product_discounted_price}}
                                    </h7>

                                </span>
                            </td>
                            <td>
                                <span>
                                    <h6>Discount after cashback</h6>
                                    {{items.product_discounted_price - Math.ceil(items.product_discounted_price*(4/100))}}
                                </span>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>





<script>
//first v-for lga kr produuct table then within again run v-for and render values of categories

import { ref } from 'vue'

    export default{
        data(){
                return{
                    categories:[],
                    products:[],
                }
            },

        setup(){
            const categories=ref([])
            const products=ref([])
            // const discountedPrice=originalPrice-(originalPrice*(10/100))
            const fetchCategory=async ()=>{
                try{
 
                    const request='http://localhost:8001/api/categories'

                    fetch(request).then((response) => {
                        response.json().then((data) => {
                            categories.value=data
                        });
                    });

                }catch(err){
                    err.value=err.message
                    
                }
            }
            
            fetchCategory()

            const fetchProduct = async () => {
                try{
                    let data=await fetch('http://localhost:8001/api/product')
                    products.value=await data.json()
                }catch(err){
                   err.value=err.message
                }

            }

            fetchProduct()
            console.log(products,'vallllllllllllllll')
            
            return {categories,products}

        },


    }
</script>


<style>
    #image{
        display: flex;
        align-items: center;
        width: 95px;
    height: 90px;    
    margin-left: 45%
    }
    #h2{
        font-family: Georgia, 'Times New Roman', Times, serif;
        font-weight: 800;
        /* font-size: 12px */
    }
</style>