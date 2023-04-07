<template>
	<div>
		<div class="card">
			<h3>Connect Wallet with @tonconnect/ui</h3>
			<div class="buttonSet">
				<button type="button" @click="connectWallet">Connect</button>
				<button type="button" @click="disconnect">Disconnect</button>
				<button type="button" @click="sendTx">Send Transaction</button>
				<button type="button" @click="checkData">Check Data</button>
			</div>
		</div>
	</div>
</template>

<script>
import { TonConnectUI } from '@tonconnect/ui';

const tonConnectUI = new TonConnectUI({
	manifestUrl: 'https://ledtorch.github.io/tonconnect-manifest.json',
	// buttonRootId: '<YOUR_CONNECT_BUTTON_ANCHOR_ID>'
	// 🚫Unreviewed
});

export default {
	name: 'TonConnect_UI',
	data() {
		return {
			walletAddress: null,
			sampleAddress: 'EQCT52hnRsePfw0XY916W8iMgdPiRByzRzFZf97VWk75MZxL',
			// TxAction: {
			// 	validUntil: Date.now() + 1000000,
			// 	messages: [
			// 		{
			// 			address:
			// 				'0:93e7686746c78f7f0d1763dd7a5bc88c81d3e2441cb34731597fded55a4ef931',
			// 			amount: '1000',
			// 			stateInit: 'base64bocblahblahblah==', // just for instance. Replace with your transaction initState or remove
			// 		},
			// 	],
			// },
		};
	},
	methods: {
		async connectWallet() {
			console.log('Conducted Button Method:');
			// Step 1
			const connectedWallet = await tonConnectUI.connectWallet(); // Call connect
		},
		async disconnect() {
			const disconnect = await tonConnectUI.disconnect();
			console.log('Disconnected');
		},
		async checkData() {
			const walletsList = await tonConnectUI.getWallets(); // Fetch wallets list
			const currentWallet = tonConnectUI.wallet;
			const currentWalletInfo = tonConnectUI.walletInfo;
			const currentAccount = tonConnectUI.account;
			const currentIsConnectedStatus = tonConnectUI.connected;
			console.log('The wallets on this device', walletsList);
			console.log('Connected wallet instance', currentWallet);
			console.log('The info of the wallet app', currentWalletInfo);
			console.log('The connected account', currentAccount);
			console.log('Connection status', currentIsConnectedStatus);

			console.log(this.payload);
			console.log(this.stateInit);
		},

		async sendTx() {
			const transaction = {
				validUntil: Date.now() + 600000, // Invalid after 10min
				messages: [
					{
						address:
							'0:93e7686746c78f7f0d1763dd7a5bc88c81d3e2441cb34731597fded55a4ef931',
						amount: '1000',
						// payload: 'BOC code',
						// This is the msg of this transaction. The BOC code tool:
						// stateInit: 'BOC Code',
						// 🚫Unreviewed ?
					},
				],
			};

			try {
				const result = await tonConnectUI.sendTransaction(transaction);

				// you can use signed boc to find the transaction
				const someTxData = await myAppExplorerService.getTransaction(
					result.boc
				);
				alert('Transaction was sent successfully', someTxData);
			} catch (e) {
				console.error(e);
			}
		},
	},
};
</script>

<style scoped>
.buttonSet {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 12px;
	gap: 24px;

	position: relative;
}
</style>
