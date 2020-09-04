<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
      
    </ul>
    <input id="mensaje" type="text" placeholder="Escribe aquí..."/>
    <button id="botonEnviar" type="button" v-on:click="soap()">Enviar</button> 
  </div>
  
    
  
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    soap: function (event) {
      // `this` inside methods points to the Vue instance
      var xmlhttp = new XMLHttpRequest();
      xmlhttp.open('POST', 'http://chat-hermes.abaigroup.com/hermes_net_v5/PlateformPublication/OnMedia/Web_Service/ChatService.asmx', true);

      // build SOAP request
      var sr =
          '<?xml version="1.0" encoding="utf-8"?>'+
          '<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">'+
          '<soap:Body>'+
              '<SendMessage xmlns="http://tempuri.org/">'+
                '<sessionId>456987123</sessionId>'+
                '<msg>PRUEBA</msg>'+
              '</SendMessage>'+
            '</soap:Body>'+
          '</soap:Envelope>';

      xmlhttp.onreadystatechange = function () {
          if (xmlhttp.readyState == 4) {
              if (xmlhttp.status == 200) {
                  alert(xmlhttp.responseText);
                  alert(xmlhttp.status);
                  // alert('done. use firebug/console to see network response');
              }
          }
      }
      // Send the POST request
      xmlhttp.setRequestHeader('Content-Type', 'text/xml; charset=utf-8');
      xmlhttp.send(sr);
  // send request
  // ...
      
    }
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
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
