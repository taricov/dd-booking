<script setup lang="ts">
import { availableLocales, loadLanguageAsync } from '~/modules/i18n'

const { t, locale } = useI18n()

async function toggleLocales() {
  // change to some real logic
  const locales = availableLocales
  const newLocale = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  await loadLanguageAsync(newLocale)
  locale.value = newLocale
}
</script>

<template>
  <nav class="mb-10 flex items-center justify-between px-20 py-5">
    <h1 class="text-xl font-bold text-gray-100">
      D-
    </h1>
    <div class="flex items-center space-x-5">
      <RouterLink icon-btn to="/" :title="t('button.home')">
        <!-- <div i-carbon-campsite /> -->
        Home
      </RouterLink>

      <RouterLink icon-btn to="/about" :title="t('button.about')">
        About
      </RouterLink>

      <RouterLink icon-btn rel="noreferrer" to="/connect">
        Connect
      </RouterLink>

      <a v-if="locale === 'en'" icon-btn :title="t('button.toggle_langs')" @click="toggleLocales()">
        <!-- <div i-carbon-language /> -->
        En
      </a>
      <a v-if="locale === 'ar'" icon-btn :title="t('button.toggle_langs')" @click="toggleLocales()">
        <!-- <div i-carbon-language /> -->
        Ar
      </a>
      <button icon-btn :title="t('button.toggle_dark')" @click="toggleDark()">
        <div i="carbon-sun dark:carbon-moon" />
      </button>
    </div>
  </nav>
</template>
