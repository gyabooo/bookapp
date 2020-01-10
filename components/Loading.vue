<template>
  <!-- <div class="loading control is-large is-loading">
  </div> -->
  <div class="loading">
    <div class="is-size-4 blinking has-text-grey-light">検索中</div>
    <a class="button is-loading is-large">
    </a>
  </div>
</template>

<script>

</script>

<style scoped>
.loading {
  text-align: center;
}
.button {
  width: 20%;
  margin: 0 auto;
}
.blinking{
	-webkit-animation:blink 1.5s ease-in-out infinite alternate;
    -moz-animation:blink 1.5s ease-in-out infinite alternate;
    animation:blink 1.5s ease-in-out infinite alternate;
}
@-webkit-keyframes blink{
    0% {opacity:0;}
    25% {opacity:1;}
    50% {opacity:0;}
    75% {opacity:1;}
    100% {opacity:0;}
}
@-moz-keyframes blink{
    0% {opacity:0;}
    25% {opacity:1;}
    50% {opacity:0;}
    75% {opacity:1;}
    100% {opacity:0;}
}
@keyframes blink{
    0% {opacity:0;}
    25% {opacity:1;}
    50% {opacity:0;}
    75% {opacity:1;}
    100% {opacity:0;}
}
</style>