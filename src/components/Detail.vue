<template>
  <div class="detail container">
    <router-link class="btn btn-default" to="/">返回</router-link>  
    <h1 class="page-header">
    	{{customer.name}}
        <span class="pull-right">
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">编辑</router-link>
            <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
        </span>
    </h1>
    <ul class="list-group">
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			电话：{{customer.phone}}
    		</span>
    	</li>
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			邮箱：{{customer.email}}
    		</span>
    	</li>
        </ul>
        <ul class="list-group">
        <li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			学历：{{customer.education}}
    		</span>
    	</li>
        <li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			毕业学校：{{customer.graduationschool}}
    		</span>
    	</li>
        <li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			职业：{{customer.profession}}
    		</span>
    	</li>
        <li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk"> 
    			个人简介：{{customer.profile}}
    		</span>
    	</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'detail',
  data () {
    return {
      customer:{}
    }
  },
  methods:{
    fetchCustomers(id){
        this.$http.get("http://localhost:3000/users/"+id)
            .then(
                function(response){
                    this.customer=response.body
                })  
    },
    deleteCustomer(id){
        this.$http.delete("http://localhost:3000/users/"+id)
            .then(function(response){
                this.$router.push({path:"/",query:{alert:"用户删除成功"}})
            })
    }
  },
  created(){
      this.fetchCustomers(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
