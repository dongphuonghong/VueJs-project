              <template>
    <h1>Thông Tin Sinh Viên</h1>
<div>
  <div>họ và tên sv:{{fullname }}</div>
  <div>ngày sinh:{{gender  }}</div>
  <div>giới tính:{{ gender }}</div>
  <div>điểm:{{ averageScore }}</div>
</div>
  <table border="1">
    <th>sản phẩm</th>
    <th>trạng thái</th>
    <th>đánh giá</th>
    <th>giá</th>
    <th>ngày</th>
    <th>thông tin</th>
    <tr>      
      <td>pc</td>
      <td>đang xử lý</td>
      <td>4</td>
      <td>10000</td>
      <td>10/10/2020</td>
      <td>
        <a href="">Xem chi tiết</a>
      </td>
    </tr>
    <th>sản phẩm</th>
    <th>trạng thái</th>
    <th>đánh giá</th>
    <th>giá</th>
    <th>ngày</th>
    <th>thông tin</th>
<tr>
  <td>laptop</td>
  <td>đang xử lý</td>
  <td>5</td>
  <td>120000</td>
  <td>10/11/2020</td>
  <td>
    <a href="">Xem chi tiết</a>
  </td>
</tr>
    <th>sản phẩm</th>
    <th>trạng thái</th>
    <th>đánh giá</th>
    <th>giá</th>
    <th>ngày</th>
    <th>thông tin</th>
  <tr v-for="(item,index) in sp " :key="index">
    <td>iPad </td>
    <td>đang xử lý</td>
    <td>5</td>
    <td>120000</td>
    <td>10/11/2020</td>
    <td>
      <a href="">Xem chi tiết</a>
    </td>
  </tr>
  <td>{{ sp.product}}</td>
  <td>{{ sp.status}}</td>
  <td>{{ sp.score}}</td>
  <td>{{ sp.price}}</td>
  <td>{{ sp.date}}</td>
  <td>{{ sp.link}}</td>
  </table>
</template>
<script>
export default {
  data() {
    return {
      sp:[{
          product:'pc',
          status:'đang xử lý',
          score:'4',
          price:'10000',
          date:'10/10/2020',
          link:'Xem chi tiết'   
        }
      ],
    fullname:'đông phương hồng đức',
            birthdate: 2003,
            gender:'Nam',
            averageScore:3.5,
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
