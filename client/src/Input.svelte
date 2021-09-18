<script>
import { socket } from "./globals";

let val = "";
let input;
</script>

<form  on:submit|preventDefault={() => {
    $socket.emit("message", val);
    input.value = "";
    val = "";

}}>
    <input type="text" bind:value={val} bind:this={input}>
</form>

<style>
    form{
        display: flex;
        justify-content: center;
        height: 87%;
    }
    input{
        position: absolute;
        width: 45rem;
        bottom: 0px;
    }

@media only screen and (max-width: 600px) {
    input {
    width: 20rem;
  }
}
</style>