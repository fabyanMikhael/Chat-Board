<!-- script -->
<script >
	import Message from "./Message.svelte";
	import Input from "./Input.svelte";
	import { io } from "socket.io-client";
	import {socket} from "./globals";


    const Socket = io("http://10.0.0.32:8080");

	let div;
	let connected = false;
	let users = 0;

	Socket.on("connect", () => {connected = true});
	Socket.on("disconnect", () => {connected = false});
	Socket.on("users", (num) => users = num);
	Socket.on("message", (message, color) => {
		const msg = document.createElement("h3");
		div.appendChild(msg);
		new Message({target: msg, props: {message, color } });
		new Audio("/pop.mp3").play();
	});
	socket.set(Socket);
</script>

<!-- html -->
<div bind:this={div}> 
	<h1>Welcome. <br> {connected ? '🟢    ' + (users <= 1 ? '' : users) : '⚫'} </h1>
	<Input/>
</div>


<!-- styling -->
<style>

@font-face {
font-family: "San Francisco";
font-weight: 400;
src: url("https://applesocial.s3.amazonaws.com/assets/styles/fonts/sanfrancisco/sanfranciscodisplay-regular-webfont.woff");
}

div{
	width: 100%;
	height: 98%;
	text-align: center;
	font-family: 'San Francisco';
	-webkit-user-select: none;
    -moz-user-select: none;
}

</style>