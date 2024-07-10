<template>
    <div>
      <v-dialog
          max-width="640px"
          v-model="dialog"
      >
          <v-card>
              <v-card-title>
                  <span>Cập nhật loại sản phẩm</span>
              </v-card-title>
              <v-card-text>
                  <v-form>
                      <v-container>
                          <v-row>
                              <v-col>
                                  <v-text-field label="Tên loại sản phẩm" v-model="data.categoryName">
                                  </v-text-field>
                              </v-col>
                          </v-row>
                      </v-container>
                  </v-form>
              </v-card-text>
              <v-divader></v-divader>
              <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="red" @click="$emit('close')">Hủy</v-btn>
                  <v-btn color="green" @click="updateCategory">Cập nhật</v-btn>
              </v-card-actions>
          </v-card>
      </v-dialog>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
      name: 'EditView',
      data(){
          return{
            data:{
                categoryId:'',
                categoryName:'',
            }
          }
      },
      props:['dialogEdit', 'currentItem'],
      computed:{
          dialog:{
              get(){
                  return this.dialogEdit;
              },
              set(value){
                  if(!value){
                      this.$emit('close');
                  }
              }
          }
      },
      methods:{
          updateCategory(){
            axios.put('https://localhost:44318/api/Category'+this.data.categoryId,this.data)
            .then(response=>{
                this.$emit('close');
                this.$emit('updateData');
                console.log(response.status);
            })
            .catch(error=>{
                console.log(error);
            })
          }
      },
      watch:{
        currentItem:function(){
            this.data.categoryId = this.currentItem.categoryId;
            this.data.categoryName = this.currentItem.categoryName;
        }
      }
  }
  </script>
  
  <style>
  
  </style>