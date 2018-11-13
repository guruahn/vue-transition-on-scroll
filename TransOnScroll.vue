<template>
  <div>
    <span class="transition-on-scroll" :class="`transition-on-scroll transition-on-scroll--${from}-${distance}__${status} ${randomId}`">
      <slot></slot>
    </span>
  </div>
</template>

<script>
export default {
  name: 'transition-on-scroll',
  props: {
    from: {
      type: String,
      default: 'top'
    },
    wrapper: {
      type: [String, Boolean],
      default: false,
      validator: function (value) {
        return !value.startsWith(".")
      }
    },
    distance: {
      type: String,
      default: 'normal',
    },
    repeat: {
      type: Boolean,
      default: false
    }
  },
  components: {

  },
  data () {
    return {
      randomId: '',
      status: 'off',
      wrapperObj: null,
      target: null,
    }
  },
  computed: {

  },

  methods: {
    randomString() {
      let chars = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXTZabcdefghiklmnopqrstuvwxyz";
      let string_length = 15;
      let randomstring = '';
      for (let i=0; i<string_length; i++) {
        let rnum = Math.floor(Math.random() * chars.length);
        randomstring += chars.substring(rnum,rnum+1);
      }
      return 'tos_' + randomstring;
    },

    isInViewport(elem, wrapperObj){
      let bounding = elem.getBoundingClientRect();
      let isInWindowView = false
      if(wrapperObj ){
        isInWindowView = bounding.top >= 0 && (bounding.top) <= wrapperObj.offsetHeight
      }else{
        isInWindowView = bounding.top >= 0 &&
        (bounding.top + 400) <= (window.innerHeight || document.documentElement.clientHeight)
      }
      return isInWindowView
    },
  },

  created(){
    this.randomId = this.randomString()
  },

  mounted(){
    let that = this
    this.$nextTick(function () {
      setTimeout(function () {
        that.target = document.querySelector('.'+that.randomId)
        if(!that.wrapper){
          that.wrapperObj = window
        }else{
          that.wrapperObj = document.querySelector('.'+that.wrapper)
        }
        that.wrapperObj.addEventListener('scroll', function () {
          if (that.isInViewport(that.target, that.wrapperObj)) {
            that.status = 'on'
          }else if(that.repeat){
            that.status = 'off'
          }
        }, 100);
      })
    })



  },

  watch: {
    // randomId: function(val){
    //   if(val) this.target = document.querySelector('.'+this.randomId)
    // }
  },

  destroyed() {
    this.wrapperObj.removeEventListener('scroll', this.onScroll)
  }


}
</script>

<style src="./TransOnScroll.scss" lang="scss">

</style>
