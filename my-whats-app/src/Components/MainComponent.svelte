<script lang="ts">
	import { writable } from 'svelte/store';
	import type { Messages } from '../types/types';
	import PopupModal from './PopupModal.svelte';

	// export let receiverName: string;
	// export let receiverImage: string;
	let isModalVisible: boolean = false;
	let message: string;
	let messageType: string;
	let receiverName=writable("");
	let receiverInput:string;
	function handleVisibility(messageTypeParam: string) {
		isModalVisible = !isModalVisible;
		messageType = messageTypeParam;
	}
	function handleReceiverNameChange(receiverInput:string){
		if(receiverInput===''||receiverInput===undefined||receiverInput===null){
            return alert('Lütfen bir isim giriniz.');
        } 
		receiverName.set(receiverInput);
	}
	const chatMessage = writable<Messages[]>([{
			messageType: 'Gönderen',
			messageContent: 'cxvx',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'werew',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'rewrwe',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'qweasd',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'xvxc',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'DFLK;GJDIOGJIOFDGJIODFJGJIODGJIDFJGJHDGJHEU4HGEUIRGHIDU',
			timeStamp: '18:17'
		},{
			messageType: 'Gönderen',
			messageContent: 'cxvx',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'werew',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'rewrwe',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'qweasd',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'xvxc',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'DFLK;GJDIOGJIOFDGJIODFJGJIODGJIDFJGJHDGJHEU4HGEUIRGHIDU',
			timeStamp: '18:17'
		},{
			messageType: 'Gönderen',
			messageContent: 'cxvx',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'werew',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'rewrwe',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'qweasd',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'xvxc',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'DFLK;GJDIOGJIOFDGJIODFJGJIODGJIDFJGJHDGJHEU4HGEUIRGHIDU',
			timeStamp: '18:17'
		},{
			messageType: 'Gönderen',
			messageContent: 'cxvx',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'werew',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'rewrwe',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'qweasd',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'xvxc',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'DFLK;GJDIOGJIOFDGJIODFJGJIODGJIDFJGJHDGJHEU4HGEUIRGHIDU',
			timeStamp: '18:17'
		},{
			messageType: 'Gönderen',
			messageContent: 'cxvx',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'werew',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'rewrwe',
			timeStamp: '18:17'
		},
		{
			messageType: 'Alıcı',
			messageContent: 'qweasd',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'xvxc',
			timeStamp: '18:17'
		},
		{
			messageType: 'Gönderen',
			messageContent: 'DFLK;GJDIOGJIOFDGJIODFJGJIODGJIDFJGJHDGJHEU4HGEUIRGHIDU',
			timeStamp: '18:17'
		}]);

	function HandleMessageCreation(content: string): any {
        if(content===''||content===undefined||content===null){
            return alert('Lütfen bir mesaj giriniz.');
        } 
		const newMessage:Messages = {
			messageType: `${messageType}`,
			messageContent: content,
			timeStamp: new Date().getHours() + ':' + new Date().getMinutes()
		};
		chatMessage.update((messages) => [...messages, newMessage]);
		console.log(chatMessage);
	}
	$: chatMessage;
</script>

<div>
	<div>
		<button on:click={() => handleVisibility('Gönderen')}>Create Receiver Message</button>
		<button on:click={() => handleVisibility('Alıcı')}>Create Sender Message</button>
		<div>
			<input placeholder="Alici Adi" bind:value={receiverInput}/>
			<button on:click={()=>handleReceiverNameChange(receiverInput)}>Alici Adini Kaydet</button>
		</div>
	</div>
</div>
<PopupModal bind:showModal={isModalVisible} {messageType}>
	<div slot="header" class="modal-dialog">
		<h5 class="modal-title">{messageType} Icin Yeni Mesaj Oluştur</h5>
	</div>
	<div slot="body" class="modal-content">
		{#if messageType === 'Gönderen'}
			<input type="text" bind:value={message} placeholder="Yeni Mesaj Gir." />
			<button on:click={() => HandleMessageCreation(message)}>Mesajı Oluştur</button>
		{/if}
		{#if messageType === 'Alıcı'}
			<input type="text" bind:value={message} placeholder="Yeni Mesaj Gir." />
			<button on:click={() => HandleMessageCreation(message)}>Mesajı Oluştur</button>
		{/if}
	</div>
</PopupModal>
<div class="chat-container">
	<div class="chat-body">
		<div class="user">
			<div class="back">
				<i class="bx bx-arrow-back"></i>
			</div>
			<div class="avatar">
				<img src="https://www.w3schools.com/w3images/avatar2.png" alt="Avatar" />
			</div>
			<div class="name">
				{#key $receiverName}
				<span>{$receiverName}</span>
				{/key}
			</div>
			<div class="options">
				<div class="video">
					<i class="bx bxs-video"></i>
				</div>
				<div class="call">
					<i class="bx bxs-phone"></i>
				</div>
				<div class="more">
					<i class="bx bx-dots-vertical-rounded"></i>
				</div>
			</div>
		</div>
		<div class="messages">

		{#key $chatMessage}
			{#each $chatMessage as message}
				<div class="message">
					{#if message.messageType === 'Gönderen'}
						<div class="divright">
							<div class="message-container">
								<p class="message-content">{message.messageContent}</p>
								<span class="timestamp-wrapper">
									<span class="timestamp">{message.timeStamp}</span>
									<span class="read"><i class="bx bx-check-double"></i></span>
								</span>
							</div>
						</div>
					{/if}
					{#if message.messageType === 'Alıcı'}
						<div class="divleft">
							<div class="message-container">
								<p class="message-content">{message.messageContent}</p>
								<span class="timestamp-wrapper">
									<span class="timestamp" style="color:lightgray">{message.timeStamp}</span>
								</span>
							</div>
						</div>
					{/if}
				</div>
			{/each}
		{/key}
	</div>

	</div>
</div>

<style>
	.messages {
    display: flex;
    flex-direction: column;
    position: relative;
    max-height: 500px; /* Set the max height to whatever height you prefer */
    overflow-y: scroll; /* Make it scrollable */
}
	.options{
		position: relative;
		left: 9%;
		display: flex;
		flex-direction: row;
		top: 10px;
	}
	.call,
	.video,
	.more {
		float: right;
	}
	.chat-container {
		position: absolute;
		top: 10%;
		width: 58%;
		max-height: 10%;
		
	}
	.avatar img {
		border-radius: 50%;
		box-shadow: 0 1px 0 rgba(255, 255, 255, 0.1);
		display: block;
		width: 100%;
	}
	.back {
		float: left;
		transform: translateY(-50%);
		position: relative;
		top: 50%;
	}
	.name {
		font-size: 17px;
		font-weight: 600;
		letter-spacing: 0.3px;
		white-space: nowrap;
		top: 10px;
		left: 10px;
		position: relative;
	}
	.avatar {
		margin: 0 0 0 5px;
		width: 36px;
		height: 36px;
	}

	.user {
		display: flex;
		height: 55px;
		background: #005e54;
		color: #fff;
		padding: 0 8px;
		font-size: 24px;
		position: relative;
		z-index: 1;
		width: 27%;
	}
	.divright {
		position: relative;
		left: 11%;
		max-width: 15%;
		padding: 10px;
		border-radius: 20px;
		margin-bottom: 10px;
		word-wrap: break-word;
		background: #e1ffc7;
		color: black;
		top: 10px;
		border-radius: 15px 0px 15px 15px;
	}
	.divleft {
		background-color: rgb(31, 44, 52);
		color: white;
		position: relative;
		max-width: 15%;
		padding: 10px;
		border-radius: 20px;
		margin-bottom: 10px;
		word-wrap: break-word;
		top: 10px;
		border-radius: 0px 15px 15px 15px;


	}
	.message-container {
		position: relative;
	}

	.message-content {
		margin-bottom: 5px;
	}
	.timestamp-wrapper .timestamp {
		color: rgba(0, 0, 0, 0.45);
		font-size: 11px;
		display: inline-block;
	}
	.timestamp-wrapper {
		display: flex;
		float: right;
		padding: 0 0 0 7px;
		position: relative;
		bottom: 4px;
	}
	.chat-body {
		display: flex;
		flex-direction: column;
		position: relative;
		max-height: 10%;
		box-shadow: inset 0 10px 10px -10px #000000;
		overflow-y: hidden;
		padding: 0 16px;
		margin-bottom: 5px;
		/* height: calc(100% - 12px); */
		position: relative;
	
	}
	.timestamp-wrapper .read {
		display: inline-block;
		margin-left: 2px;
		position: relative;
		bottom: 5px;
		height: 16px;
		width: 16px;
	}
	.read {
		color: lightblue;
	}
</style>
