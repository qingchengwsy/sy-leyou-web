<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        this.$http.post("/item/category/add",node)
          .then(({data})=>{
          if (data===true){
            alert("添加成功");
          }else{
            alert("添加失败");
          }
        });
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name)
        this.$http.post("/item/category/update",id,name);
      },
      handleDelete(id) {
        this.$http.get("/item/category/delete/"+id)
        .then(({data})=>{
          if (data===true){
            console.log("delete---"+data)
          }
        });
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
