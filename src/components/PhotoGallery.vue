<template>
  <div ref="gallery" >
    <a v-for="(image, key) in props.pics" :key="key" :href="`${cloudinaryUrl}c_scale,w_${props.fullSize}/${props.quality}${props.album}/${image.name}.jpg`" :data-pswp-width="image.width"
      :data-pswp-height="image.height" target="_blank" rel="noreferrer">
      <img :src="`${cloudinaryUrl}c_scale,w_${props.thumbSize}/${props.quality}${props.album}/${image.name}.jpg`" alt="" />
    </a>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import PhotoSwipeLightbox from 'photoswipe/lightbox';
import 'photoswipe/style.css';

const cloudinaryUrl = 'https://res.cloudinary.com/periphic/image/upload/';
const gallery = ref(null);
const props = defineProps({
  pics: Array,
  quality: {
    type: String,
    default: 'q_auto/f_auto/'
  },
  thumbSize: {
    type: Number,
    default: 500,
  },
  fullSize: {
    type: Number,
    default: 2000,
  },
  album: {
    type: String,
  }
});

// const images = [
//   {
//     largeURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/1/img-2500.jpg',
//     thumbnailURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/1/img-200.jpg',
//     width: 1875,
//     height: 2500,
//   },
//   {
//     largeURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/2/img-2500.jpg',
//     thumbnailURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/2/img-200.jpg',
//     width: 1669,
//     height: 2500,
//   },
//   {
//     largeURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/3/img-2500.jpg',
//     thumbnailURL:
//             'https://cdn.photoswipe.com/photoswipe-demo-images/photos/3/img-200.jpg',
//     width: 2500,
//     height: 1666,
//   },
// ];

onMounted(() => {
  console.log('mounted')
  console.log(props.photos)
  const lightbox = new PhotoSwipeLightbox({
    gallery: gallery.value,
    // gallery: '#gallery--getting-started',
    children: 'a',
    pswpModule: () => import('photoswipe'),
  });
  lightbox.init();
})

onUnmounted(() => {
  if (this.lightbox) {
    console.log('unmounted')
    this.lightbox.destroy();
    this.lightbox = null;
  }
})

</script>
