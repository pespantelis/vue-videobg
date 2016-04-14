<template>
  <section class="VideoBg">
    <video autoplay loop muted v-el:video>
      <source v-for="source in sources" :src="source" :type="getMediaType(source)">
    </video>
    <slot></slot>
  </section>
</template>


<script>
  export default {
    props: {
      sources: {
        type: Array,
        required: true
      },
      img: {
        type: String
      }
    },

    data () {
      return {
        videoRatio: null
      }
    },

    ready () {
      this.setImageUrl()
      this.setContainerHeight()

      if (this.videoCanPlay()) {
        this.$els.video.oncanplay = () => {
          this.videoRatio = this.$els.video.videoWidth / this.$els.video.videoHeight
          console.log(this.videoRatio)
          this.setVideoSize()
          this.$els.video.style.visibility = 'visible'
        }
      }

      window.addEventListener('resize', this.resize)
    },

    beforeDestroy () {
      window.removeEventListener('resize', this.resize)
    },

    methods: {
      resize () {
        this.setContainerHeight()

        if (this.videoCanPlay()) {
          this.setVideoSize()
        }
      },

      videoCanPlay () {
        return !!this.$els.video.canPlayType
      },

      setImageUrl () {
        if (this.img) {
          this.$el.style.backgroundImage = `url(${this.img})`
        }
      },

      setContainerHeight () {
        this.$el.style.height = `${window.innerHeight}px`
      },

      setVideoSize () {
        var width, height, containerRatio = this.$el.offsetWidth / this.$el.offsetHeight

        if (containerRatio > this.videoRatio) {
          width = this.$el.offsetWidth
        } else {
          height = this.$el.offsetHeight
        }

        this.$els.video.style.width = width ? `${width}px` : 'auto'
        this.$els.video.style.height = height ? `${height}px` : 'auto'
      },

      getMediaType (src) {
        return 'video/' + src.split('.').pop()
      }
    }
  }
</script>


<style>
  .VideoBg {
    position: relative;
    background-size: cover;
    background-position: center;
    overflow: hidden;
  }

  .VideoBg video {
    position: absolute;
    top: 50%;
    left: 50%;
    visibility: hidden;
    transform: translate(-50%, -50%);
  }
</style>
