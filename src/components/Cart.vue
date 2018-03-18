<template>
<div>
    <div class="ui fluid container grid">
        <div class="nine wide column">
            <div class="ui segment">
                <div class="ui three cards">
			        <div class="card" v-for="item in items" :key="item.id">
                        <div class="image">
                            <img :src="item.img">
                        </div>
			            <div class="content">
				            <div class="header">{{ item.name }}</div>
				            <div class="description">
				                <p class="itemprice">₱ {{ item.price }}.00</p>
				            </div>
			            </div>
			            <button type="button" class="ui bottom green attached button" @click="addItem(item)">
				            <i class="add icon"></i>
				            Add to Cart
			            </button>
			        </div>
			    </div>
            </div>         
        </div>
        <div class="seven wide column">
            <div class="ui segment">
			    <h3 class="ui dividing header">Your Cart</h3>
                <div class="ui middle aligned divided list">
                <div v-if="cart.length > 0">
                <table class="ui small table">
                    <thead>
                    <tr>
                        <th>Item Name</th>
                        <th>Price</th>
                        <th>Quantity</th>
                        <th>Total</th>
                        <th></th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="item in cart" :key="item.id">
                        <td>{{ item.name }}</td>
                        <td>₱ {{ item.price }}.00</td>
                        <td>x{{ item.quantity }}</td>
                        <td>₱ {{ item.price * item.quantity }}.00</td>
                        <td>
                        <div class="ui small basic icon buttons">
                            <button class="ui button" @click="removeItem(item)">
                            <i class="trash icon"></i>
                            </button>
                            <button class="ui button" @click="incrementItem(item)">
                            <i class="plus icon"></i>
                            </button>
                            <button class="ui button" @click="decrementItem(item)">
                            <i class="minus icon"></i>
                            </button>
                        </div>
                        </td>
                    </tr>
                    </tbody>
                    <tfoot>
                    <tr>
                        <td></td>
                        <td></td>
                        <td>Total Price</td>
                        <td class="totalprice">₱ {{ totalprice }}.00</td>
                    </tr>
                    </tfoot>
                </table>
                <button type="submit" class="ui fluid blue button">Checkout</button>
                </div>
                <div v-else>
                    <div class="ui info message">
                        <p>No item/s in cart</p>
                    </div>
                </div>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Cart',
    data () {
        return {
            cart: [],
            items: [
                { id: 1, name: 'T-Shirt #1', price: '150', quantity: 1, img: './static/imgs/t-shirt1.jpg'},
                { id: 2, name: 'T-Shirt #2', price: '170', quantity: 1, img: './static/imgs/t-shirt2.jpg'},
                { id: 3, name: 'T-Shirt #3', price: '200', quantity: 1, img: './static/imgs/t-shirt3.jpg'},
                { id: 5, name: 'T-Shirt #4', price: '200', quantity: 1, img: './static/imgs/t-shirt4.jpg'},
                { id: 6, name: 'T-Shirt #5', price: '160', quantity: 1, img: './static/imgs/t-shirt5.jpg'},
                { id: 7, name: 'T-Shirt #6', price: '220', quantity: 1, img: './static/imgs/t-shirt6.jpg'}
            ],

        }
    },
    computed: {
        totalprice () {
            return this.cart.reduce((accum, product) => {
            return accum + product.price * product.quantity
            }, 0)
        }

    },
    methods: {
        addItem (item) {
            const record = this.cart.findIndex(p => {
                return p.id === item.id
            })

            if(record === -1) {
                this.cart.push(item)
            }
            else {
                item.quantity += 1
            }
        },
        removeItem (item) {
            const record = this.cart.findIndex(p => {
                return p.id === item.id
            })
            this.cart.splice(record, 1)
        },
        decrementItem (item) {
            const record = this.cart.findIndex(p => {
                return p.id === item.id
            })

            if(this.cart[record].quantity <= 1) {
                this.cart.splice(record, 1)
            }
            else {
                item.quantity -= 1
            }
        },
        incrementItem (item) {
            item.quantity += 1
        }
    }
}
</script>
<style>
.itemprice {

    color: olivedrab;
    font-size: 15px;
    font-weight: bold;
    float: right;

}

.totalprice {

    color: orangered;
    font-weight: bold;

}
</style>