<script>
  let plantHeight = 0
  function hide(elementId){
    let element = document.getElementById(elementId)
    if (element.classList.contains("hidden")){
      return
    }
    else{
      element.classList.add("hidden")
    }
  }
  function unHide(elementId){
    let element = document.getElementById(elementId)
    if (element.classList.contains("hidden")){
      element.classList.remove("hidden")

    }
    else{
      return
    }
  }

  class Task {
    name = "";
    amountToGoUp = 1;
    progress = 0;
    selected = false;
    id = "";
    completeions = 0;
   

    constructor(id, name, amountToGoUp,plantHeightIncrement,unlockHeight) {
      this.name = name;
      this.amountToGoUp = amountToGoUp;
      this.id = id;
      this.plantHeightIncrement = plantHeightIncrement
      this.unlockHeight = unlockHeight
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
      if (this.selected == false) {
        this.amountToGoUp = 0;
      } else {
        this.progress += this.amountToGoUp;
        this.progress = this.progress
        // Reset progress and change style instantly after reaching 100%
        if (this.progress >= 100) {
          this.progress = 0;
          this.completeions ++;
          plantHeight += this.plantHeightIncrement;
 
          console.log(this.completeions)
        }
        const progressButton = document.getElementById(this.id);
        let progressString = this.progress.toString() + "%";
        progressButton.style.width = progressString;
      }
    }
  }

  let tasks = [];
  tasks.push(new Task("1", "Water", 0.5, 1,0));
  tasks.push(new Task("2", "Fertilize soil", 0.25,3,5));
  


 
  setInterval(function () {
    if (tasks.length > 0) {      
      tasks.forEach((task) => {
        // if task is unlocked/display
        //if (task is not displayed && task.getUnlockHeight == plantHeight) {
          // do stuff
        //}
        
        
        if(task.unlockHeight > plantHeight){
          hide(task.id)
        }
        

        if (task.isSelected()) {
          task.incrementProgress();
        }
      });
    }
  }, 10);
</script>
<div class="center">
<p class="text">Plant height: {plantHeight}</p></div>
{#each tasks as task}
  <button
    class="button"
    on:click={function () {
      task.flipSelected();
    }}
  >
   {task.name}
    <div class="outer">
      <div 
        class="inside"
        id="{task.id}"
        style="width: {task.getProgress()}%"
      ></div>
    </div>
  </button>
{/each}
