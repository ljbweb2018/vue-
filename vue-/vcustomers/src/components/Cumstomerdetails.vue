<template>
    <div class="details container">
      <router-link to="/" class="btn btn-default">
        <span class="glyphicon glyphicon-menu-left">返回</span>
      </router-link>
      <h1 class="page-header">{{ customer.name }}
        <span class="pull-right">
          <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
            编辑
          </router-link>
          <button class="btn btn-banger" v-on:click="deleteCustomer(customer.id)">
            删除
          </button>
        </span>
      </h1>
      <ul class="list-group">
        <li class="list-group-item"><span class="
glyphicon glyphicon-earphone"></span><span class="mar">{{ customer.phone }}</span></li>
        <li class="list-group-item"><span class="
glyphicon glyphicon-envelope"></span><span class="mar">{{ customer.email }}</span></li>
      </ul>
      <ul class="list-group">
        <li class="list-group-item"><span class="
glyphicon glyphicon-star-empty"></span><span class="mar">{{ customer.education }}</span></li>
        <li class="list-group-item"><span class="
glyphicon glyphicon-flag"></span><span class="mar">{{ customer.graduationschool }}</span></li>
        <li class="list-group-item"><span class="
glyphicon glyphicon-asterisk"></span><span class="mar">{{ customer.profession }}</span></li>
        <li class="list-group-item"><span class="
glyphicon glyphicon-user"></span><span class="mar">{{ customer.porfile }}</span></li>
      </ul>
    </div>
</template>

<script>
    export default {
      name: "Cumstomerdetails",
      data () {
        return {
          customer: ""
        }
      },
      methods:{
        fetchCustomers(id) {
          this.$http.get("http://localhost:3000/users/"+id)
            .then(function (response) {
              // console.log(response);
              this.customer = response.body;
            })
        },
        deleteCustomer(id) {
          var r=confirm("确认删除？");
          if (r==true){
            this.$http.delete("http://localhost:3000/users/"+id)
              .then(function (response) {
                // console.log(response);
                this.$router.push({path:"/",query:{alert:"用户删除成功"}})
              })
          }
        },
      },
      created() {
        this.fetchCustomers(this.$route.params.id)
      }
    }
</script>

<style scoped>
  .mar{
    display: inline-block;
    padding-left: 10px;
  }
</style>
