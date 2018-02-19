<template>
  <div class="what">
    <div v-html="content[1].htmlcontent"></div>
  </div>
</template>

<script>
export default {
  name: 'ContentContainer',
  props: {
    msg: String,
  },
  data: function () {
    return {
      content: []
    }
  },
  mounted: function(){
    this.$http.get('http://matthewlissner.com/wp-json/wp/v2/hot_sauces?filter[orderby]=date&order=asc').then(response => {
      let y = this;
      response.body.forEach(function(val){
        y.content.push({htmlcontent: val.content.rendered})
        console.log(y.content)
      })
    }, () => {
      console.log('sorry about that');
      this.isActive = true;
      // error callback
    });
  },
}
</script>
