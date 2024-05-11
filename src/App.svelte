<script>
  let progress = 0;
let taps = 0
  let selected = false;
  let clicks = 3;
  let amountToGoUp = 1

  
  setInterval(function(){
      
      if (selected == true) {
      progress += amountToGoUp


      // Reset progress and change style instantly after reaching 100%
      if (progress >= 100) {
            progress = 0;
          taps ++
            const pbInside = document.getElementById("progressBarInside");
            if (pbInside.classList.contains("inside")) {
              pbInside.classList.remove("inside");
              pbInside.classList.add("inside2");
            }
       

      }}
    }, 20    
    )
  function barSpeed() {
    selected = !selected;
    if(selected == false){
      const pbInside = document.getElementById("progressBarInside");
      pbInside.classList.replace("inside","inside2")
    }
   }


</script>

<button class="button" on:click={function () { barSpeed();bind:clicks += 1;}}>
  Get water for your plant
  <p>{taps}</p>
  <div class="outer" id="progressBarOutside">
    <div class="inside" id="progressBarInside" style="width: {progress}%"></div>
  </div>
</button>
