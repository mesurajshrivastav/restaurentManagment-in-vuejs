<template>
 <router-view/>
</template>

<script>

export default {
  name: 'App',
}
</script>

<style>
body {
    margin : 0;
    padding : 0;
}
.box {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: -45px;
}

.content {
    margin-top: -80px;
}

.fields  {
    display: flex;
    flex-direction: column;
    width: 400px;
    margin: auto;
}

.fields input {
    padding: 5px;
    margin: 5px;
}

.fields button {
    width: 390px;
    padding: 5px;
    margin: 5px;
}

.logo {
    width: 250px;
}
</style>
