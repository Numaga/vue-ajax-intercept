<template>
  <div></div>
</template>
<script>
export default {
    name: "AjaxIntercept",
    mounted() {
      var listener = { 
        tempOpen: XMLHttpRequest.prototype.open,
        tempSend: XMLHttpRequest.prototype.send,
      }, eu = this;

      XMLHttpRequest.prototype.open = function(a='',b='') {
        listener.tempOpen.apply(this, arguments);
        eu.$emit('start', this);

        this.addEventListener('load', function() {
            eu.$emit('finish', this);
        });
      }
    }
}
</script>