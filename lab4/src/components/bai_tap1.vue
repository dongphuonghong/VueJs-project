<template>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap...in.css">
    <div class="row">
        <div class="col-4 text-center">
            <img :src="require(`@/assets/image/${imgs}`)" style="width: 100%; height: 400px;">
            <div class="row" style="margin-top: 10px;">
                <div class="col-3" v-for="item in ImgV" :key="item">
                    <a href="#">
                        <img :src="require(`@/assets/image/${item}`)" style="width:70%" @click="changeImg(item)">
                    </a>
                </div>
            </div>
        </div>
        <div class="col-5">
            <h1>{{ title() }}</h1>
            <span>
                <i class="fas fa-star" v-for="k in starRating()" :key="k"></i>
            </span>
            <div class="text-justify">
                {{ Content }}
            </div>
            <h3>GIÁ BÁN : {{ formattedPrice }}</h3>
            <strong v-if="inSale()">Giá khuyến mãi: {{ priceOnSale() }}</strong>
            <strong v-else>Giá khuyến mãi đã hết !</strong>
            <h5>Số sản phẩm còn trong kho : {{ inStock() }}</h5>
            <button class="btn btn-primary" @click="addCart(selectedVariant)" :disabled="inStock() === 0">Mua liền
                !</button>
            <br>
            <br>
            <a href="#" v-for="(item, index) in products" :key="index" @click="selectedVariant = index; ChangeImage()">
                <img :src="require(`@/assets/image/${item.img}`)" style="width: 20%; margin: 20px;">
            </a>
        </div>
        <div class="col-3">
            <div style="border: 1px solid black; margin-top: 10px; padding: 10px;">
                <a href="#" style="float: left;">
                    <i class="fas fa-shopping-cart" style="font-size: 50px;"></i>
                </a>
                <div class="text-center">
                    {{ totalItems() }}<br>
                    Tổng tiền : {{ Total() }} <br>
                    <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
                        view cart
                    </button>
                </div>
            </div>
            <div style="border: 1px solid black; margin-top: 10px; padding: 10px;" class="text-center">
                <div class="card" style="width: 100%;">
                    <div class="card-header">
                        Chủng loại
                    </div>
                    <ul class="list-group list-group-flush">
                        <li class="list-group-item bg-primary ">Điện thoại di động</li>
                        <li class="list-group-item bg-secondary ">Máy tính xách tay</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
    <!-- -->
    <!-- Modal -->
    <!-- Button trigger modal -->
    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <table style="width: 800px;" class="table">
                        <thead>
                            <tr>
                                <th>HÌNH</th>
                                <th>SẢN PHẨM</th>
                                <th>ĐƠN GIÁ</th>
                                <th>SỐ LƯỢNG</th>
                                <th>THÀNH TIỀN</th>
                                <th></th>
                            </tr>
                            <tr v-for="(item, index) in cart" :key="index">
                                <td><img :src="require(`@/assets/image/${item.img}`)" style="height: 100px; width: 100px;">
                                </td>
                                <td class="align-middle">{{ item.name }}</td>
                                <td class="align-middle">{{ item.price }}</td>
                                <td class="align-middle">{{ item.quality }}</td>
                                <td class="align-middle">{{ item.price * item.quality }}</td>
                                <td class="align-middle">
                                    <button class="btn btn-danger" @click="Remove(index)">xóa 1</button>
                                </td>
                            </tr>
                            <tr>
                                <th></th>
                                <th></th>
                                <th>Tổng tiền </th>
                                <th> {{ totalItems() }}</th>
                                <th>{{ Total() }}</th>
                            </tr>
                        </thead>
                    </table>
                </div>
                <div class="modal-body">

                </div>
                <div class="modal-footer">
                    <th><button class="btn btn-danger" @click="DeleteAll()">Xóa hết</button></th>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
export default {
    name: "l3Compomemt",
    data() {
        return {
            ImgV: ['1.jpg', '2.jpg', '3.jpg', '4.jpg'],
            Content: 'Là dòng sản phẩm có thiết kế mỏng nhẹ, sang trọng và tinh tế cùng với đó là giá thành phải chăng nên MacBook Air đã thu hút được đông đảo người dùng yêu thích và lựa chọn. Một trong những phiên bản mới nhất mà khách hàng không thể bỏ qua khi đến với CellphoneS đó là MacBook Air M1. Dưới đây là chi tiết về thiết kế, cấu hình của máy.',
            products: [
                { img: '1.jpg', name: 'Apple MacBook Air M1 256GB 2020 I I Chính hãng Apple Việt Nam ', price: 26500, rating: 3, inStock: 5, color: 'Đen', onSale: true, quality: 0 },
 
{ img: '5.jpg', name: 'Apple MacBook Air 13 256GB 2020 I I Chính hãng Apple Việt Nam ', price: 29500, rating: 4, inStock: 3, color: 'Xanh', onSale: false, quality: 0 },
                { img: '6.jpg', name: 'Apple MacBook Air 13 512GB 2020 I I Chính hãng Apple Việt Nam ', price: 30500, rating: 5, inStock: 0, color: 'Cam', onSale: true, quality: 0 }
            ],
            selectedVariant: 0,
            cart: [],
            imgs: '1.jpg'
        }
    },
    computed: {
        formattedPrice() {
            return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(this.price());
        }
    },
    methods: {
        changeImg(img) {
            this.imgs = img;
        },
        title() {
            return this.products[this.selectedVariant].name;
        },
        starRating() {
            return Array(this.products[this.selectedVariant].rating).fill(0);
        },
        price() {
            return this.products[this.selectedVariant].price;
        },
        priceOnSale() {
            return this.products[this.selectedVariant].onSale ? this.products[this.selectedVariant].price : '';
        },
        inSale() {
            return this.products[this.selectedVariant].onSale;
        },
        inStock() {
            return this.products[this.selectedVariant].inStock;
        },
        addCart(selectedVariant) {
            if (this.inStock() > 0) {
                const itemIndex = this.cart.findIndex(item => item.name === this.products[selectedVariant].name);
                if (itemIndex === -1) {
                    this.cart.push({ ...this.products[selectedVariant], quality: 1 });
                } else {
                    this.cart[itemIndex].quality++;
                }
                this.products[selectedVariant].inStock--;
            }
        },
        totalItems() {
            return this.cart.reduce((total, item) => total + item.quality, 0);
        },
        Total() {
            return this.cart.reduce((total, item) => total + (item.price * item.quality), 0);
        },
        Remove(index) {
            if (this.cart[index].quality > 1) {
                this.cart[index].quality--;
            } else {
                // Nếu số lượng sản phẩm chỉ còn 1, xóa sản phẩm khỏi giỏ hàng
                this.products.forEach(product => {
                    if (product.name === this.cart[index].name) {
                        product.inStock++;
                    }
                });
                this.cart.splice(index, 1);
            }
        },

        DeleteAll() {
            this.cart.forEach(item => {
                this.products.forEach(product => {
                    if (product.name === item.name) {
                        product.inStock += item.quality;
                    }
                });
            });
            this.cart = [];
        },
        ChangeImage() {
            this.imgs = this.products[this.selectedVariant].img; 
}
    }
};
</script>
<style scoped>
.thumbnail-images {
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
}

.thumbnail {
    width: 50px;
    height: auto;
    cursor: pointer;
}

.thumbnail:hover {
    opacity: 0.7;
}
</style>