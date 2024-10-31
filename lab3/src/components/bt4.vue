<template>
    <div class="hello">
        <h1>Bai 4</h1>
        <nav class="navbar navbar-expand-lg bg-body-tertiary">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">Navbar</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Link</a>
                        </li>
                        <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"
                                aria-expanded="false">
                                Dropdown
                            </a>
                            <ul class="dropdown-menu">
                                <li><a class="dropdown-item" href="#">Action</a></li>
                                <li><a class="dropdown-item" href="#">Another action</a></li>
                                <li>
                                    <hr class="dropdown-divider">
                                </li>
                                <li><a class="dropdown-item" href="#">Something else here</a></li>
                            </ul>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link disabled" aria-disabled="true">Disabled</a>
                        </li>
                    </ul>
                    <form class="d-flex" role="search">
                        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#searchModal">
                            Tìm kiếm
                        </button>
                        <!-- Modal -->
                        <div class="modal fade" id="searchModal" tabindex="-1" aria-labelledby="searchModalLabel"
                            aria-hidden="true">
                            <div class="modal-dialog">
                                <div class="modal-content">
                                    <div class="modal-header">
                                        <h1 class="modal-title fs-5" id="exampleModalLabel">Tìm Kiếm sản phẩm</h1>
                                        <button type="button" class="btn-close" data-bs-dismiss="modal"
09:02
 
aria-label="Close"></button>
                                    </div>
                                    <div class="modal-body">
                                        <div class="d-flex" role="search">
                                            <input v-model="searchQuery" class="form-control me-2" type="search"
                                                placeholder="Search" aria-label="Search">
                                        </div>

                                        <div>
                                            <template v-if="hasFilteredProducts && searchQuery.trim() !== ''">
                                                <div v-for="item in filteredProducts" :key="item.id">
                                                    <img :src="item.image" class="card-img-top" alt="">
                                                    <div class="card-body">
                                                        <h5 class="card-title">{{ item.name }}</h5>
                                                        <p class="card-text">{{ item.price }}</p>
                                                        <div class="btn btn-success" @click="addTocart(item)">Mua</div>
                                                    </div>
                                                </div>
                                            </template>
                                            <template v-else>
                                                <p v-if="searchQuery.trim() !== ''">No matching products found.</p>
                                            </template>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>



                        <!-- giỏ hàng -->
                        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#cartModal">
                            Giỏ hàng
                        </button>
                        <!-- Modal -->
                        <div class="modal fade" id="cartModal" tabindex="-1" aria-labelledby="cartModalLabel"
                            aria-hidden="true">
                            <div class="modal-dialog">
                                <div class="modal-content">
                                    <div class="modal-header">
                                        <h1 class="modal-title fs-5" id="exampleModalLabel">Giỏ hàng</h1>
                                        <button type="button" class="btn-close" data-bs-dismiss="modal"
                                            aria-label="Close"></button>
                                    </div>
                                    <div v-for="(cartItem, index ) in cart" :key="cartItem.id">
                                        <div class="modal-body">
 
<table class="table">
                                                <thead>
                                                    <tr>
                                                        <th scope="col">Hình</th>
                                                        <th scope="col">Sản phẩm</th>
                                                        <th scope="col">Đơn giá</th>
                                                        <th scope="col">Số lượng</th>
                                                        <th scope="col">Tiền</th>
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                    <tr>
                                                        <th scope="row"><img :src="cartItem.image" alt="" srcset=""
                                                                width="100px"></th>
                                                        <td>{{ cartItem.name }}</td>
                                                        <td>{{ cartItem.price }}</td>
                                                        <td class="d-flex">
                                                            <div class="btn btn-danger" @click="giamsoluongsp(index)">-
                                                            </div>
                                                            {{ cartItem.soluong }}
                                                            <div class="btn btn-danger" @click="tangsoluongsp(index)">+
                                                            </div>
                                                        </td>
                                                        <td>
                                                            {{ cartItem.soluong * cartItem.price }}
                                                        </td>
                                                        <div class="btn btn-danger" @click="Xoa1sp(index)">Xóa
                                                        </div>
                                                    </tr>
                                                </tbody>
                                            </table>
                                        </div>
                                    </div>
                                    <div>
                                        <p>Tổng sản phẩm: {{ totalQuantity }} </p>
                                        <p>Tổng tiền: {{ tinhtongtien() }}</p>
                                        <button type="button" class="btn btn-secondary"
                                            data-bs-dismiss="modal">Close</button>
                                        <div class="btn btn-danger" @click="deleteAll">Xóa
                                            hết</div>
 
</div>
                                </div>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </nav>
        <div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: space-around">
            <div v-for="item in mang" :key="item.id">
                <div class="card" style="width: 18rem;">
                    <img :src="item.image" class="card-img-top" alt="">
                    <div class="card-body">
                        <h5 class="card-title">{{ item.name }}</h5>
                        <p class="card-text">{{ item.price }}</p>
                        <div class="btn btn-success" @click="addTocart(item)">Mua</div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
  
<script>
export default {
    name: 'bai4Components',
    data() {
        return {
            mang: [
                {
                    name: "Đồng hồ thụy sỹ",
                    image: "https://i.pinimg.com/564x/79/dc/01/79d...27.jpg",
                    price: 1200,
                    soluong: 1
                },
                {
                    name: "Dell Star X",
                    image: "https://i.pinimg.com/736x/65/7b/8e/657...84.jpg",
                    price: 700,
                    soluong: 1
                },
                {
                    name: "Sony Vaio 2017",
                    image: "https://i.pinimg.com/736x/0d/1a/3f/0d1...fb.jpg",
                    price: 1700,
                    soluong: 1
                },
                {
                    name: "Máy ảnh Canon",
                    image: "https://i.pinimg.com/736x/f7/6f/a4/f76...09.jpg",
                    price: 300,
                    soluong: 1
                },
                {
                    name: "Vòng cưới France",
                    image: "https://i.pinimg.com/564x/1f/04/d3/1f0...48.jpg",
                    price: 7000,
                    soluong: 1
                },
                {
                    name: "Motorola thế hệ 5",
                    image: "https://i.pinimg.com/564x/76/33/cf/763...2e.jpg",
                    price: 900,
                    soluong: 1
                },
                {
                    name: "Mũ cao bồi Mexico",
                    image: "https://i.pinimg.com/564x/6a/b8/f7/6ab...d6.jpg",
                    price: 100,
                    soluong: 1
                },
                {
                    name: "Nước hoa Korea",
                    image: "https://i.pinimg.com/736x/d0/43/ae/d04...ea.jpg",
                    price: 600,
                    soluong: 1
                }
 
],
            cart: [],
            tongtien: 0,
            searchQuery: ''


        }
    },
    computed: {
        totalCosts() {
            return this.cart.map(item => item.soluong * item.price);
        },
        totalQuantity() {
            return this.cart.reduce((total, item) => total + item.soluong, 0);
        },
        filteredProducts() {
            // Check if searchQuery is defined and not null
            if (!this.searchQuery || typeof this.searchQuery !== 'string') {
                return this.mang; // Return all products if the search query is not a string
            }

            // Chuyển đổi searchQuery thành chữ thường và loại bỏ khoảng trắng
            const lowercaseQuery = this.searchQuery.toLowerCase().trim();

            // Sử dụng filter để lọc các sản phẩm có tên, số hoặc giá chứa chuỗi tìm kiếm
            return this.mang.filter(item => {
                const itemName = (item.name || '').toLowerCase(); // Ensure item.name is defined
                const itemNumber = item.number !== undefined ? item.number.toString() : ''; // Ensure item.number is defined
                const itemPrice = item.price !== undefined ? item.price.toString() : ''; // Ensure item.price is defined

                return (
                    itemName.includes(lowercaseQuery) ||
                    itemNumber.includes(lowercaseQuery) ||
                    itemPrice.includes(lowercaseQuery)
                );
            });
        },



        hasFilteredProducts() {
            return this.filteredProducts.length > 0;
        },
    },
    methods: {
        addTocart(item) {
            // Check if the item is already in the cart
            const existingItem = this.cart.find(cartItem => cartItem.name === item.name);

            if (existingItem) {
                // Increment the quantity if the item is already in the cart
                existingItem.soluong += 1;
            } else {
                // Add a new entry to the cart if the item is not already present
                this.cart.push({ ...item, soluong: 1 });
            }
        },
        deleteAll() {
            this.cart = []
        },
        Xoa1sp(index) {
            this.cart.splice(index, 1)
        },
        tangsoluongsp(index) {
            this.cart[index].soluong += 1;
        },
        giamsoluongsp(index) {
            if (this.cart[index].soluong > 1) {
                this.cart[index].soluong -= 1;
            } else {
                this.cart.splice(index, 1);
            }
        },
        tinhtongtien() {
            let tong = 0;
            for (const totalCost of this.totalCosts) {
                tong += totalCost;
            }
            return tong;
        },
        tim_sp() {
            console.log(`Searching for: ${this.searchQuery}`);
        }




    },
}
</script>