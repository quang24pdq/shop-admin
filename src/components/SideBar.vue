<template>
    <v-navigation-drawer>
        <v-toolbar color="blue">
            <v-icon class="ml-2">mdi-home</v-icon>
            <v-toolbar-title>QUẢN TRỊ SHOP</v-toolbar-title>
        </v-toolbar>
        <v-list>
            <v-list-subheader>DANH MỤC</v-list-subheader>
            <v-list-item
                v-for="(item, i) in link"
                :key="i"
                :value="item"
                color="blue"
            >
                <template v-slot:prepend>
                    <v-icon :icon="item.icon"></v-icon>
                </template>
                <v-list-item-title>{{item.text}}</v-list-item-title>
            </v-list-item>
        </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
    name: 'SideBar',
    data(){
        return{
            link:[
            {icon:'mdi-microsoft-windows', text:'Loại sản phẩm'},
            {icon:'mdi-khanda', text:'Sản phẩm'},
            {icon:'mdi-calendar', text:'Đơn hàng'},
            {icon:'mdi-flask', text:'Chi tiết đơn hàng'},
            {icon:'mdi-chart-pie', text:'Người dùng'},
            {icon:'mdi-chat', text:'Khách hàng'},
            ]
        }
    }

}
</script>

<style>

</style>