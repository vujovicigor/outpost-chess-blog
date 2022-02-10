<script>
	import { onMount } from 'svelte';
	let eyeBall, pupil, eyeArea,pupilArea,R, r, centerX, centerY, eventListener;
	function onMouseMove(e){
		let x = e.clientX - centerX,
				y = e.clientY - centerY,
				theta = Math.atan2(y,x),
				angle = theta*180/Math.PI + 360;
		pupil.style.transform = `translateX(${R - r +"px"}) rotate(${angle + "deg"})`;
		pupil.style.transformOrigin = `${r +"px"} center`;
	}
	
	onMount(() => {
		eyeArea = eyeBall.getBoundingClientRect()
    pupilArea = pupil.getBoundingClientRect()
    R = eyeArea.width/2
    r = pupilArea.width/2
    centerX = eyeArea.left + R
    centerY = eyeArea.top + R
		console.log(eyeArea,pupilArea,R, r, centerX, centerY)
		document.addEventListener("mousemove", onMouseMove);
		
		return function(){console.log('removed event ',  onMouseMove);document.removeEventListener("mousemove", onMouseMove)}
	});

</script>
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg" width="100" height="100" class="eye">
  <circle cx="50" cy="50" r="50" fill="#fff" class="eyeball" bind:this={eyeBall} />
  <circle cx="50" cy="50" r="24" fill="#0D0D20" class="pupil" bind:this={pupil} />
</svg>
<style>
.eye{
  margin: auto;

/*   background:#ccc; */
}
.pupil{
  position:relative;
   transform:  rotate(15deg); 
/*   transform-origin: 20px center; */
}
</style>