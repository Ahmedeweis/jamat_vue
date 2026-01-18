<template>
  <div :dir="dir">
    <router-view />
  </div>
</template>
<script setup>
import { computed, watch } from 'vue'
import { useI18n } from 'vue-i18n'
import { useHead } from '@vueuse/head'
import { SecureEnvironment } from './services/axios'

SecureEnvironment.syncState();

useHead({
  title: 'JAMAAT | منصة الألعاب العربية',
  meta: [
    { name: 'description', content: 'JAMAAT: منصة عربية مخصصة للألعاب التعليمية والترفيهية. استمتع بتحميل مباشر، تجربة سهلة، وتحديات يومية.' },
    { property: 'og:title', content: 'JAMAAT - منصتك للألعاب' },
    { property: 'og:description', content: 'تجربة ألعاب فريدة، تحميل مباشر، وسهولة في الاستخدام. انضم إلى عالم JAMAAT الآن!' },
    { property: 'og:image', content: 'https://jamaat-gilt.vercel.app/src/assets/imgs/j.png' },
    { property: 'og:url', content: 'https://jamaat-gilt.vercel.app/' },
    { property: 'og:type', content: 'website' }
  ]
})

const { locale } = useI18n()
// كل ما اللغة تتغير، الاتجاه يتحدث فوراً
const dir = computed(() => (locale.value === 'ar' ? 'rtl' : 'ltr'))
watch(locale, (newLang) => {
  document.dir = newLang === 'ar' ? 'rtl' : 'ltr'
  document.documentElement.lang = newLang
})
</script>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
