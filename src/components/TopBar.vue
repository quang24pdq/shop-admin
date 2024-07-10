<template>
  <v-app-bar color="blue">
    <v-app-bar-nav-icon> </v-app-bar-nav-icon>
    <v-spacer></v-spacer>
    <v-toolbar-icon>
        <v-btn>Hire me</v-btn>
        <v-btn>Blog</v-btn>
        <v-btn>
            <v-icon>mdi-cat</v-icon>
        </v-btn>
        <v-btn>
            <v-badge color="red" content="5">
                <v-icon>mdi-bell</v-icon>
            </v-badge>
        </v-btn>
        <v-btn>
            <v-avatar>
                <v-img
                    src="https://inkythuatso.com/uploads/thumbnails/800/2022/05/meo-khoc-nhu-nguoi-11-08-57-55.jpg"
                    alt="Ánh"
                ></v-img>
            </v-avatar>
        </v-btn>
    </v-toolbar-icon>
  </v-app-bar>
</template>

<script>
export default {
    name: 'TopBar'

}
</script>

<style>

</style>