<script setup lang="ts">
// defineComponents({})
defineOptions({
  name: 'IndexPage',
})
const user = useUserStore()
const name = ref(user.savedName)

const router = useRouter()
function go() {
  if (name.value)
    router.push(`/hi/${encodeURIComponent(name.value)}`)
}

const { t } = useI18n()
</script>

<template>
  <!-- <div class="!text-6xl mx-auto my-20 font-bold flex items-center justify-center">D-Booking</div> -->
  <div
    href="#"
    class="mb-7 inline-flex items-center justify-between rounded-full bg-gray-100 px-4 py-1 text-sm text-gray-700 dark:bg-gray-800 hover:bg-gray-200 dark:text-white dark:hover:bg-gray-700"
    role="alert"
  >
    From checkout to global sales tax compliance, companies
  </div>

  <div class="option-group">
    <div class="option-container">
      <input id="option-1" class="option-input" checked type="radio" name="options">
      <input id="option-2" class="option-input" type="radio" name="options">

      <label class="option !bg-gray-800/30" for="option-1">
        <span class="option__indicator" />

        <span class="option__label">
          <sub class="!text-[0.3em]">One-Time</sub>
        </span>
      </label>

      <label class="option !bg-gray-800/30" for="option-2">
        <span class="option__indicator" />
        <span class="option__label">
          <sub class="">Range</sub>
        </span>
      </label>
    </div>
  </div>

  <!--
	<div>
	<div text-4xl>
	<div i-carbon-campsite inline-block />
	</div>
	<p>
	<em text-sm opacity-75>{{ t('intro.desc') }}</em>
	</p>

	<div py-4 />

	<TheInput
	v-model="name"
	:placeholder="t('intro.whats-your-name')"
	autocomplete="false"
	@keydown.enter="go"
	/>
	<label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>

	<div>
	<button
	m-3 text-sm btn
	:disabled="!name"
	@click="go"
	>
{{ t('button.go') }}
</button>
</div>
</div>
-->
  <!-- <input :key="i" type="checkbox" for="i in 10" :id=`checkbox_${i}`>{{"checkbox" + i}}</input> -->
  <TheChip />
</template>

<route lang="yaml">
meta:
layout: home
</route>

<style scoped>
html {
	background: linear-gradient(to bottom, #4678F3, #64D6EE);
	font-size: 62.5%;
	height: 100%;
	display: flex;
}

body {
	width: 100%;
	margin: auto;
}

.option-group {
	width: 90%;
	max-width: 400px;
	height: 150px;
	position: relative;
	overflow: hidden;
	border-radius: 0.25em;
	font-size: 4rem;
	margin: 0.2em auto;
	transform: translateZ(0);
}

.option-container {
	display: flex;
	justify-content: center;
	align-items: stretch;
	width: 120%;
	height: 100%;
	margin: 0 -10%;
}

.option {
	overflow: hidden;
	flex: 1;
	display: block;
	padding: 0.5em;
	background: #64D6EE;
	position: relative;
	margin: 0em;
	margin-right: 0.2em;
	border-radius: 0.25em;
	display: flex;
	justify-content: flex-end;
	align-items: flex-start;
	flex-direction: column;
	cursor: pointer;
	opacity: 0.5;
	transition-duration: 0.8s, 0.6s;
	transition-property: transform, opacity;
	transition-timing-function: cubic-bezier(.98, 0, .22, .98), linear;
	will-change: transform, opacity;
}

.option:last-child {
	margin-right: 0;
}

.option__indicator {
	display: block;
	background: #000;

	transform-origin: left bottom;
	transition: inherit;
	will-change: transform;
	position: absolute;
	top: 0.5em;
	right: 0.5em;
	left: 0.5em;
}

.option__indicator:before,
.option__indicator:after {

	display: block;
	border: solid 2px #585757;
	border-radius: 50%;
	width: 0.25em;
	height: 0.25em;
	position: absolute;
	top: 0;
	right: 0;
}

.option__indicator:after {
	@apply bg-white;
	background: #000;
	transform: scale(0);
	transition: inherit;
	will-change: transform;
}

.option-input {
	position: absolute;
	top: 0;
	z-index: -1;
	visibility: hidden;
}

.option__label {
	display: block;
	width: 100%;
	text-transform: uppercase;
	font-size: 1.5em;
	font-weight: bold;
	transform-origin: left bottom;
	transform: translateX(20%) scale(0.7);
	transition: inherit;
	will-change: transform;
}

.option__label sub {
	font-size: 0.4em;
}

.option__label:after {
	@apply  dark:border-white;

	content: '';
	display: block;
	border: solid 2px #000000;
	width: 100%;
	transform-origin: 0 0;
	transform: scaleX(0.2);
	transition: inherit;
	will-change: transform;
}

.option:last-child .option__label {
	transform: translateX(0%) scale(0.7);
}

.option:last-child .option__indicator {
	transform: translateX(-20%);
}

.option-input:checked~.option {
	transform: translateX(-20%) translateX(0.2em);
}

.option-input:checked~.option .option__indicator {
	transform: translateX(0%);
}

.option-input:checked~.option .option__label {
	transform: translateX(40%) scale(0.7);
}

.option-input:first-child:checked~.option {
	transform: translateX(20%) translateX(-0.2em);
}

.option-input:first-child:checked~.option .option__indicator {
	transform: translateX(-40%);
}

.option-input:first-child:checked~.option .option__label {
	transform: translateX(0%) scale(0.7);
}

.option-input:nth-child(1):checked~.option:nth-of-type(1),
.option-input:nth-child(2):checked~.option:nth-of-type(2) {
	opacity: 1;
}

.option-input:nth-child(1):checked~.option:nth-of-type(1) .option__indicator,
.option-input:nth-child(2):checked~.option:nth-of-type(2) .option__indicator {
	transform: translateX(0);
}

.option-input:nth-child(1):checked~.option:nth-of-type(1) .option__indicator::after,
.option-input:nth-child(2):checked~.option:nth-of-type(2) .option__indicator::after {
	transform: scale(1);
}

.option-input:nth-child(1):checked~.option:nth-of-type(1) .option__label,
.option-input:nth-child(1):checked~.option:nth-of-type(1) .option__label::after,
.option-input:nth-child(2):checked~.option:nth-of-type(2) .option__label,
.option-input:nth-child(2):checked~.option:nth-of-type(2) .option__label::after {
	transform: scale(1);
}
</style>
