<template>
	<div>
		<div class="card">
			<h3>Connect Wallet with @tonconnect/SDK</h3>
			<button type="button" @click="connectWallet">Connect Wallet</button>
		</div>
	</div>
</template>

<script>
import { TonConnect } from '@tonconnect/sdk';
const connector = new TonConnect({
	manifestUrl: 'https://viutila.github.io/tonconnect-manifest.json',
});

export default {
	name: 'TonConnect_SDK',
	data() {
		return {
			walletAddress: null,
			sampleAddress: 'EQDT5CMUBQOdzKPS8LE053px7csibOaNNoIbeKRq_tm9YRDA',
		};
	},
	methods: {
		async connectWallet() {
			console.log('Conducted Button Method:');
			// Step 1

			connector.restoreConnection();
			// If the user connected the wallet, this restores the connection.
			const walletsList = await connector.getWallets();
			// const unsubscribe = connector.onStatusChange();

			const unsubscribe = connector.onStatusChange((walletInfo) => {
				console.log('Connection status:', walletInfo);
			});

			const selectedWallet = walletsList[0];
			if (selectedWallet.injected) {
				connector.connect({ jsBridgeKey: selectedWallet.jsBridgeKey });
			} else {
				const walletConnectionSource = {
					universalLink: selectedWallet.universalLink,
					bridgeUrl: selectedWallet.bridgeUrl,
				};
				const universalLink = connector.connect(walletConnectionSource);
				// Use the universalLink to show a QR code or as a deep link
			}
			// const unsubscribe = connector.onStatusChange((walletInfo) => {
			// 	console.log('Connection status:', walletInfo);
			// });
			connector.restoreConnection();
			console.log(unsubscribe);
			console.log(walletsList);
			console.log('jsBridgeKey:', walletsList[0].jsBridgeKey);
			console.log('universalLink:', walletsList[0].universalLink);
			// connector.connect({ jsBridgeKey: walletsList[0].jsBridgeKey });
			// connector.connect({ jsBridgeKey: walletsList[0].universalLink });
			// connector.connect({ jsBridgeKey: 'tonkeeper' });
			// connector.connect({ bridgeUrl: 'https://bridge.tonapi.io/bridge' });
		},
	},
};
</script>

<style lang="scss" scoped></style>
