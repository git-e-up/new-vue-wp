<template>

  <!-- <h1>{{ svg }}</h1> -->
  <span v-html="myFace"></span>

</template>

<script>
export default {
  name: 'MyFace',
  // props: {
  //   svg: String
  // },
  data() {
    return {
      myFace: ''
    }
  },
  mounted: function(){
    this.$http.get('http://matthewlissner.com/wp-json/wp/v2/svgs/name').then(response => {
      let a = this;
      console.log(response);
      let promise1 = Promise.resolve(response.text())
      promise1.then(function(value){
        // console.log(value)
        a.myFace = value
      })
    }, () => {
      console.log('failedddd')
    });
  }
}
</script>

<style lang="scss">
$off-white: rgb(243, 242, 237);
$blue-steel: #607d8b;
$screen-sm-min: 768px;
$screen-md-min: 992px;
$screen-lg-min: 1200px;

.hide {
  display: none;
}

#matt-img {
  position: absolute;
  top: 0;
  right: 0;
  display: inline-block;
  height: 100%;
  max-width: 30%;
  @media(min-width: $screen-sm-min){
      max-width: 15%;
  }
  cursor: pointer;
  path {
    stroke: $blue-steel;
    stroke-width: 20;
    stroke-dasharray: 8000;
    stroke-dashoffset: 8000;
    animation: drawMatt 4s 1 linear;
    animation-fill-mode: forwards;
  }
  &:active {

    path {
      animation: drawMatt2 4s 1 ease;
      animation-fill-mode: forwards;
    }
  }
}

@keyframes drawMatt {
  to {
    stroke-dashoffset: 0;
    fill: $blue-steel;
    fill-opacity: 1;
  }
}
@keyframes drawMatt2 {
  to {
    stroke-dashoffset: 0;
    fill: $blue-steel;
    fill-opacity: 1;
  }
}

</style>
