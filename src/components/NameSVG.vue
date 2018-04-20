<template>

  <!-- <h1>{{ svg }}</h1> -->
  <span v-html="myName"></span>

</template>

<script>
export default {
  name: 'MyName',
  // props: {
  //   svg: String
  // },
  data() {
    return {
      myName: ''
    }
  },
  mounted: function(){
    this.$http.get('http://matthewlissner.com/wp-json/wp/v2/svgs/matthew').then(response => {
      let a = this;
      let promise1 = Promise.resolve(response.text())
      promise1.then(function(value){
        console.log(value)
        a.myName = value
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

#matthew-svg {
  max-width: 60%;
  max-height: 95%;
  position: relative;
  display: inline-block;
  cursor: pointer;
  @media(min-width: $screen-sm-min) {
      max-width: 40%;
  }
  path {
    fill-opacity: 0;
    stroke: $blue-steel;
    stroke-width: 2;
    stroke-dasharray: 870;
    stroke-dashoffset: 870;
    animation: drawSVG 4s 1 linear;
    animation-fill-mode: forwards;
  }
  &:active {

    path {
      animation: drawSVG2 4s 1 ease;
      animation-fill-mode: forwards;
    }
  }
}

@keyframes drawSVG {

  to {
    stroke-dashoffset: 0;
    fill: $blue-steel;
    fill-opacity: 1;
  }
}
@keyframes drawSVG2 {
  to {
    stroke-dashoffset: 0;
    fill: $blue-steel;
    fill-opacity: 1;
  }
}


</style>
