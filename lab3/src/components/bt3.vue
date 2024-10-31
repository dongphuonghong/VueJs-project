<template>
    <div class="hello">
        <h1>thông tin</h1>
        <div class="card-header">
            danh sách hàng hóa
        </div>
        <div class="card-body">
            <table class="table">
                    <thead>
                        <tr>
                            <th scope="col">San pham</th>
                            <th scope="col">Don gia</th>
                            <th scope="col">Giam gia</th>
                            <th scope="col">Ngay</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in products" :key="item.id">
                            <th class="sanpham">{{ item.sanpham }}</th>
                            <th class="dongia">{{ formatCurrency(item.dongia) }}</th>
                            <th>{{ sale1(item.giamgia) }}</th>
                            <th>{{ item.ngay }}</th>
                        </tr>
                    </tbody>
                </table>
        </div>
    </div>
    <div class="card-footer" id="icon">
                <button type="button" class="btn btn-danger" @click="sortTable('sanpham')"><i
                        class="bi bi-hand-index"></i> sắp sếp cột sản phẩm</button>
                <button type="button" class="btn btn-danger" @click="sortTable('dongia')" id="left"><i
                        class="bi bi-hand-index"></i> sắp sếp cột đơn giá</button>
                <button type="button" class="btn btn-danger" @click="sortTable('giamgia')" id="right"><i
                        class="bi bi-hand-index"></i> sắp sếp cột giảm giá></button>
                <button type="button" class="btn btn-danger" @click="sortTable('ngay')" id="bot"><i
                        class="bi bi-hand-index"></i> sắp sếp ngày</button>
            </div>
</template>
<script>
export default {
name: 'bt3Components', 
    data(){
        return {
            products: [
            { sanpham: "aniseed syrup", dongia: "190", giamgia: 19, ngay: "March-16,2000" },
            { sanpham: "change", dongia: "280", giamgia: 0, ngay: "December-3,2000" },
            { sanpham: "aniseed syrup", dongia: "245", giamgia: 0, ngay: "June-21,2000" },
            { sanpham: "cheft action's cajun seasoning", dongia: "366", giamgia: 0, ngay: "July-10,2000" },
            { sanpham: "cheft action's gumbo mix", dongia: "154", giamgia: 0, ngay: "September-16,2000" },
            { sanpham: "grandma's boysenberry spread", dongia: "222", giamgia: 3, ngay: "March-16,2000" },
            { sanpham: "uncle's boysenberry spread", dongia: "365", giamgia: 3, ngay: "March-11,2000" },            
],
sortColumn: '',
        sortDirection: 'asc',
        }
    },
    methods: {
        formatCurrency(value) {
            return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
        },
        sale1(value){
return value/100;
        },
        sortTable(column) {
            if (this.sortColumn === column) {
            this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
        } else {
            this.sortColumn = column;
            this.sortDirection = 'asc';
        }
        this.products.sort((a,b) =>{
            const modifier = this.sortDirection === 'desc' ? -1 : 1;
            if (a[column] < b[column]) {
                return -1 * modifier;
            }
            if (a[column] > b[column]) {
                return 1 * modifier;
            }
        
        })
        }
    }
}
</script>