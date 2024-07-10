<template>
  <div>
    <v-row class="mt-3">
        <v-icon>mdi-home</v-icon>
        <h3 class="ml-2">Danh sách loại sản phẩm</h3>
        <v-spacer></v-spacer>
        <v-btn
        icon
        color="blue"
        size="small"
        @click="dialogAdd=true"
        >
        <v-icon>mdi-plus</v-icon>
        </v-btn>
    </v-row>
    <v-row class="mt-1">
        <v-col>
            <v-card>
                <v-table>
                    <thead>
                        <tr>
                            <th>STT</th>
                            <th>Mã loại sản phẩm</th>
                            <th>Tên loại sản phẩm</th>
                            <th>Chức năng</th>
                            
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item,index) in categories" :key="index">
                            <td>{{ index+1 }}</td>
                            <td>{{ item.categoryId }}</td>
                            <td>{{ item.categoryName }}</td>
                            <td>
                                <v-btn
                                    color="blue"
                                    class="mr-3"
                                    icon
                                    size="x-small"
                                    @click="dialogEdit=true,
                                        currentItem = item"
                                >
                                    <v-icon>mdi-pencil</v-icon>
                                </v-btn>
                                <v-btn
                                    color="red"
                                    class="mr-3"
                                    icon
                                    size="x-small"
                                    @click="dialogDelete=true, categoryId=item.categoryId"
                                >
                                    <v-icon>mdi-delete</v-icon>
                                </v-btn>
                            </td>

                        </tr>
                    </tbody>
                </v-table>
            </v-card>
        </v-col>
    </v-row>
    <add-view
        :dialogAdd="dialogAdd"
        @close="dialogAdd=false"
        @updatData="getCategories"
    />
    <edit-view
        :dialogEdit = "dialogEdit"
        @close="dialogEdit=false"
        @updateData="getCategories"
        :currentItem ="currentItem"
    />
    <v-dialog
        max-width="400px"
        v-model="dialogDelete"
    >
        <v-card>
            <v-alert type="error">
                <v-row align="center">
                    <v-col cols="11" class="text-center">
                        Bạn có đồng ý xóa không ?
                    </v-col>
                </v-row>
                <v-row align="center">
                    <v-col cols="6">
                        <v-btn 
                        variant="text"
                        @click="deleteCategory"
                        >Đồng ý</v-btn>
                    </v-col>
                    <v-col cols="6">
                        <v-btn 
                        variant="text"
                        @click="dialogDelete=false"
                        >Hủy bỏ</v-btn>
                    </v-col>
                </v-row>
            </v-alert>
        </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from 'axios'
import AddView from './AddView.vue'
import EditView from '../EditView.vue'
export default {
  components: { AddView, EditView },
    name:'ListView',
    data(){
        return{
            categories:[],
            dialogAdd: false,
            dialogEdit: false,
            currentItem:'',
            dialogDelete: false,
            categoryId:'',
        };
    },
    methods:{
        getCategories(){
            axios.get('https://localhost:44318/api/Category')
            .then(response=>{
                this.categories = response.data;

            }).catch(error=>{
                console.log(error);
            })
        },
        deleteCategory(){
            axios.delete('https://localhost:44318/api/Category' +categoryId)
            .then(response=>{
                var newArr = this.categories.filter(x= x.categoryId != this.categoryId);
                this.categories = newArr;
                this.$emit('close');
            })
        }
    },
    created(){
        this.getCategories();
    }
}
</script>

<style>

</style>