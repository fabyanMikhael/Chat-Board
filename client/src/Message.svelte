<script>
import { onMount } from "svelte";
export let message;
export let color = {r: 0, g: 0, b: 0};
let self;
onMount(() => {
    const x = Math.random() * (50) + 20;
    const y = Math.random() * (50) + 20;
    self.style.top = `${y}%`;
    self.style.left = `${x}%`;
    self.style.color = `rgb(${color.r}, ${color.g}, ${color.b})`;
    setTimeout(() => {self.remove()}, 3900);
});

</script>


<h3 bind:this={self}>{message}</h3>

<style>
    h3{
        animation: FadeOut 4s forwards;
        position: absolute;
        font-size: x-large;
        text-shadow: 1px 0 0 #000, 0 -1px 0 #000, 0 1px 0 #000, -1px 0 0 #000;
        -webkit-user-select: none;
        -moz-user-select: none;
    }
    @keyframes FadeOut{
        0% {opacity: 100%;}
        100% {opacity: 0%;}
    }
</style>