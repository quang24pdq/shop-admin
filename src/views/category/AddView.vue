<template>
  <div>
    <v-dialog
        max-width="640px"
        v-model = "dialog"
    >
    <v-card>
        <v-card-title>
            <span>Thêm mới loại sản phẩm</span>
        </v-card-title>
        <v-card-text>
            <v-form>
                <v-container>
                    <v-row>
                        <v-col>
                            <v-text-field
                            label = "Tên loại sản phẩm"  
                            v-model="data.categoryName"  
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-container>
            </v-form>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
            color="gray"
            @click="$emit('close')"
            >Hủy</v-btn>
            <v-btn
            color="primary"
            @click="addCategory"
            >Lưu</v-btn>
        </v-card-actions>
    </v-card>

    </v-dialog>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name:'AddView',
    data(){
        return{
            data:{
                categoryName: ''
            }
        }
    },
    props:['dialogAdd'],
    computed:{
        dialog:{
            get(){
                return this.dialogAdd;
            },
            set(value){
                if(!value){
                    this.$emit('close');
                }
            }
        }
    },
    methods:{
        addCategory(){
            axios.post("https://localhost:44318/api/Category")
            .then(response =>{
                this.$emit('close');
                this.$emit('updateData');
                console.log(response.status);
            })
            .catch(error =>{
                console.log(error);
            })
        }
    }
}
</script>

<style>

</style>