<script>
  let plantHeight = 0;
  let power = 100;
  let growthPerSecond = 0;
  let leaves = 0
  let soldLeaves = 0
  function hide(elementId) {

  console.log("Element:", document.getElementById(elementId)); // Log the element
  if (document.getElementById(elementId.toString()).classList.contains("hidden")) {
    return;
  } else {
    document.getElementById(elementId.toString()).classList.add("hidden");
  }
}

  function unHide(elementId) {

  if (document.getElementById(elementId.toString()) !== null && document.getElementById(elementId).classList.contains("hidden")) {
    document.getElementById(elementId.toString()).classList.remove("hidden");
  }
}


  class Task {
    name = "";
    amountToGoUp = 1;
    progress = 0;
    selected = false;
    id = "";
    turns = 0;

    constructor(
      id,
      name,
      amountToGoUp,
      plantHeightIncrement,
      unlockHeight,
      buttonId,
      completeions,
      cost,
      gps
    ) {
      this.cost = cost
      this.name = name;
      this.amountToGoUp = amountToGoUp;
      this.id = id;
      this.plantHeightIncrement = plantHeightIncrement;
      this.unlockHeight = unlockHeight;
      this.buttonId = buttonId;
      this.completeions = completeions
      this.gps = gps
    }

    isSelected() {
      return this.selected;
    }

    setSelected() {
      this.selected = true;
    }

    flipSelected() {
      this.selected = !this.selected;
    }

    setUnSelected() {
      this.selected = false;
    }

    setAmountToGoUp(newAmountToGoUp) {
      this.amountToGoUp = newAmountToGoUp;
    }

    getProgress() {
      return this.progress;
    }

   
    incrementProgress() {
      
      if(this.progress == 1 ){
        power -= this.cost
      }
      
    
      if (this.selected == false) {
        this.amountToGoUp = 0;
      } else {
        this.progress += this.amountToGoUp;
        this.progress = this.progress;
        
      
        // Reset progress and change style instantly after reaching 100%
        if (this.progress >= 100) {
          this.progress = 0;
          this.completeions++;
          this.completeions = this.completeions
          

          console.log(this.completeions);
        }
        const progressButton = document.getElementById(this.id);
        let progressString = this.progress.toString() + "%";
        progressButton.style.width = progressString;
      }
    }
  }


  let tasks = [];
  tasks.push(new Task("1", "Water Bees", 0.5, 1, 0,"a",0,5,0.2));
 setInterval(function(){
  tasks.forEach((task) => {
plantHeight += task.gps/4 * task.completeions
growthPerSecond = findGrowthPerSecond()
growthPerSecond = growthPerSecond
  })
 },250)
 function findGrowthPerSecond() {
  growthPerSecond = 0
  tasks.forEach((task) => {
  
    growthPerSecond += task.gps * task.completeions
  })
  return growthPerSecond

 }
 
function findLeaves(){
  leaves = plantHeight/4
  
}
function sellLeaves(){
  power += soldLeaves *2

}
  setInterval(function () {
    if(power <= 0){
      return
    }
    if (tasks.length > 0) {
      tasks.forEach((task) => {
        task.completeions = task.completeions
        tasks = tasks

        // if task is unlocked/display
        //if (task is not displayed && task.getUnlockHeight == plantHeight) {
        // do stuff
        //}
        if(tasks.length <= 1){
          if(plantHeight>= 5){
            tasks.push(new Task("2", "Soil Fertilizing Bees", 0.25, 3, 5,"b",0,10,0.5));
            tasks = tasks

           
          }}





        if (task.isSelected()) {
          task.incrementProgress();
        }
      });
    }
  }, 10);
</script>
<p class="text"> Power: {power}</p>
<p class="text">Growth per second: {growthPerSecond.toFixed(2)}</p>
<div class="center">
  <p class="text">Plant height: {plantHeight.toFixed(2)}</p>
</div>

{#each tasks as task}
  <button
    class="button"
    on:click={function () {
      task.flipSelected();
 
    }}
  >
<p >{task.completeions}</p>
    {task.name}
    <div class="outer">
      <div
        class="inside"
        id={task.id}
        style="width: {task.getProgress()}%"
      ></div>
    </div>
  </button>
{/each}

