<template>
  <div class="hello">
    {{ beforeMount.title }}
  </div>
</template>

<script>
/* esLint-disable */
let Feed = require("rss-to-json");
var $ = require('jquery');

export default {
  name: "HelloWorld",

  data() {
    return {
      msg: "Welcome to Your RSS Feed"
    };
  },   
   beforeMount () {
        var self = this
        $(document).ready(function () {
         var feed = 'http://todayilearned.dk/feed.xml';
         $.ajax(feed, {
           accepts: {
             xml: 'application/rss+xml'
           },
           dataType: 'xml',
           success: function (data) {
             $(data).find('item').each(function () {
               var el = $(this);
               self.title = el.find('title').text()
               console.log('title      : ' + el.find('title').text());
               console.log('link       : ' + el.find('link').text());
               console.log('description: ' + el.find('description').text());
             });
           }
         });
       });
     }
 };
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
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
