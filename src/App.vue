<script setup>
import HelloWorld from './components/HelloWorld.vue';
import ConnectWalletSDK from './components/ConnectWalletSDK.vue';
import ConnectWalletUI from './components/ConnectWalletUI.vue';
</script>

<template>
	<div>
		<a href="https://vitejs.dev" target="_blank">
			<img src="/vite.svg" class="logo" alt="Vite logo" />
		</a>
		<a href="https://vuejs.org/" target="_blank">
			<img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
		</a>
	</div>
	<HelloWorld />
	<div class="frame">
		<ConnectWalletSDK />
		<ConnectWalletUI />
	</div>
</template>

<style scoped>
.logo {
	height: 3em;
	padding: 0.5em;
	will-change: filter;
	transition: filter 300ms;
}
.logo:hover {
	filter: drop-shadow(0 0 1em #646cffaa);
}
.logo.vue:hover {
	filter: drop-shadow(0 0 1em #42b883aa);
}

.frame {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: flex-start;
}
</style>
