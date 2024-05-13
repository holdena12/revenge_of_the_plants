<script>
  let plantHeight = 0;
  let power = 50;
  let growthPerSecond = 0;
  let leaves = 0;
  let soldLeaves = 0;
  function hide(elementId) {
    let elem = document.getElementById(elementId);
    if (elem.classList) {
      if (!elem.classList.contains("hidden")) {
        elem.classList.add("hidden");
      }
    }
  }
  function unhide(elementId) {
    let elem = document.getElementById(elementId);

    if (elem.classList.contains("hidden")) {
      elem.classList.remove("hidden");
    }
  }
  class Task {
    unlocked = true;
    name = "";
    amountToGoUp = 1;
    progress = 0;
    selected = false;
    id = "";
    turns = 0;
    ogAmountToGoUp = this.amountToGoUp;

    constructor(
      id,
      name,
      amountToGoUp,
      plantHeightIncrement,
      unlockHeight,
      buttonId,
      completeions,
      cost,
      gps,
      toolTipText,
    ) {
      this.cost = cost;
      this.name = name;
      this.amountToGoUp = amountToGoUp;
      this.id = id;
      this.plantHeightIncrement = plantHeightIncrement;
      this.unlockHeight = unlockHeight;
      this.buttonId = buttonId;
      this.completeions = completeions;
      this.gps = gps;
      this.toolTipText = toolTipText;
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
      if (this.progress == 1) {
        power -= this.cost;
        this.amountToGoUp = this.ogAmountToGoUp;
      }
      if (power < this.cost) {
        isReset();
      }

      if (this.selected == false) {
        this.amountToGoUp = 0;
      } else {
        this.progress += this.amountToGoUp;

        this.progress = this.progress;

        // Reset progress and change style instantly after reaching 100%
        if (this.progress >= 100) {
          this.progress = 0;
          let audio = new Audio ("696660__ajgrf__wet-plunger-click.wav")

          this.completeions++;
          this.completeions = this.completeions;

          console.log(this.completeions);
        }
        const progressButton = document.getElementById(this.id);
        let progressString = this.progress.toString() + "%";
        progressButton.style.width = progressString;
      }
    }
  }

  function isUnlocked() {
    tasks.forEach((task) => {
      if (task.unlockHeight >= plantHeight) return (task.unlocked = true);
      else return (task.unlocked = false);
    });
  }
  function isReset() {
    tasks.forEach((task) => {
      task.unlockHeight = 1000000000000000;
      task.completeions = 0;
      task.progress = 0;
      task.selected = false;
    });
    tasks = [];
    tasks.push(
      new Task(
        "1",
        "Water Bees",
        0.5,
        1,
        0,
        "a",
        0,
        5,
        0.2,
        "Collecting bees to get water for your plant, copsts 5 power per bee.",
      ),
    );
    isUnlocked();
    plantHeight = 0;
    power = 50;
    growthPerSecond = 0;
    document.getElementById("log").innerText =
      "Log: started the game\nLog: Do not run out of power it will reset you";
  }

  let tasks = [];
  tasks.push(
    new Task(
      "1",
      "Water Bees",
      0.5,
      1,
      0,
      "a",
      0,
      5,
      0.2,
      "Collecting bees to get water for your plant, copsts 5 power per bee.",
    ),
  );

  setInterval(function () {
    if (growthPerSecond >= 50) unhide("sellLeaves10");
    if (growthPerSecond >= 200) unhide("sellLeaves100");

    tasks.forEach((task) => {
      plantHeight += (task.gps / 4) * task.completeions;
      growthPerSecond = findGrowthPerSecond();
      growthPerSecond = growthPerSecond;
      findLeaves();
    });
  }, 250);
  function findGrowthPerSecond() {
    growthPerSecond = 0;
    tasks.forEach((task) => {
      growthPerSecond += task.gps * task.completeions;
    });
    return growthPerSecond;
  }

  function findLeaves() {
    leaves = plantHeight / 10;

    leaves = leaves;
  }
  function sellLeaves() {
    if (plantHeight >= 10) {
      power += soldLeaves * 4;
      plantHeight -= soldLeaves * 10;
    }
    plantHeight = plantHeight;
    soldLeaves = 0;

    power = power;
  }
  setInterval(function () {
    if (power <= 0) {
      isReset();
    }
    if (tasks.length > 0) {
      tasks.forEach((task) => {
        task.completeions = task.completeions;
        tasks = tasks;

        // if task is unlocked/display
        //if (task is not displayed && task.getUnlockHeight == plantHeight) {
        // do stuff
        //}

        if (tasks.length <= 1) {
          if (plantHeight >= 5) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Soil Fertilizing Bees",
                0.25,
                3,
                5,
                "b",
                0,
                10,
                0.5,
                "Collecting bees that ferilize the soil for your plant, costs 10 power per bee.",
              ),
            );

            tasks = tasks;
          }
        }
        if (tasks.length <= 2) {
          if (plantHeight >= 50) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Sun light bees",
                0.25,
                3,
                5,
                "b",
                0,
                50,
                4,
                "Collecting bees that will bring sunlight to your plant to help it grow faster, cost per bee 50 power.",
              ),
            );
          }
        }
        if (tasks.length <= 3) {
          if (plantHeight >= 500) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Pollination Bees",
                0.25,
                3,
                5,
                "b",
                0,
                500,
                6,
                "Pollination bees help increase the yield of your plant's fruits and flowers. Cost per bee: 500 power.",
              ),
            );
          }
        }

        if (tasks.length <= 4) {
          if (plantHeight >= 1000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Guardian Bees",
                0.25,
                3,
                5,
                "b",
                0,
                1000,
                10,
                "Guardian bees protect your plant from pests and diseases, ensuring its health. Cost per bee: 1000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 5) {
          if (plantHeight >= 5000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Harvesting Bees",
                0.25,
                3,
                5,
                "b",
                0,
                5000,
                12,
                "Harvesting bees help gather ripe fruits and flowers from your plant. Cost per bee: 5000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 6) {
          if (plantHeight >= 10000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Nectar Bees",
                0.25,
                3,
                5,
                "b",
                0,
                10000,
                14,
                "Nectar bees enhance the sweetness and flavor of your plant's fruits and flowers. Cost per bee: 10000 power.",
              ),
            );
          }
        }
        if (tasks.length <= 7) {
          if (plantHeight >= 30000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Pollen Bees",
                0.25,
                3,
                5,
                "b",
                0,
                30000,
                16,
                "Pollen bees help in cross-pollination, resulting in stronger and healthier plants. Cost per bee: 30000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 8) {
          if (plantHeight >= 30000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Frost Protection Bees",
                0.25,
                3,
                5,
                "b",
                0,
                50000,
                18,
                "Frost protection bees shield your plant from cold weather damage, ensuring its survival. Cost per bee: 50000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 9) {
          if (plantHeight >= 250000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Aroma Bees",
                0.25,
                3,
                5,
                "b",
                0,
                250000,
                20,
                "Aroma bees enhance the fragrance of your plant's flowers, attracting beneficial insects. Cost per bee: 2500000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 10) {
          if (plantHeight >= 500000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Growth Accelerator Bees",
                0.25,
                3,
                5,
                "b",
                0,
                500000,
                22,
                "Growth accelerator bees significantly boost the growth rate of your plant. Cost per bee: 500000 power.",
              ),
            );
          }
        }

        if (tasks.length <= 11) {
          if (plantHeight >= 1000000) {
            document.getElementById("log").innerText +=
              "\n Log: You have unlocked a new kind of bee";
            tasks.push(
              new Task(
                "2",
                "Rainbow Bees",
                0.25,
                3,
                5,
                "b",
                0,
                1000000,
                24,
                "Rainbow bees bring vibrant colors to your plant, making it visually appealing. Cost per bee: 1000000 power.",
              ),
            );
          }
        }

        tasks = tasks;

        if (task.isSelected()) {
          task.incrementProgress();
        }
      });
    }
  }, 10);
</script>

<div class="center">
  <div class="top-bar">
    <div class="top-bar-button">
      <button
        id="sellLeaves"
        on:click={() => {
          if (soldLeaves <= leaves) {
            soldLeaves += 1;
            sellLeaves();
          }
        }}
        title={"Sell leaves to increase your power, costs ten plant height."}
        class="leaveButton"
        >Sell leaves
      </button>
      <button
        id="sellLeaves10"
        on:click={() => {
          if (soldLeaves <= leaves) {
            soldLeaves += 10;
            sellLeaves();
          }
        }}
        title={"Sell leaves to increase your power, costs ten plant height."}
        class="leaveButton hidden"
        >Sell leaves 10
      </button>
      <button
        id="sellLeaves100"
        on:click={() => {
          if (soldLeaves <= leaves) {
            soldLeaves += 100;
            sellLeaves();
          }
        }}
        title={"Sell leaves to increase your power, costs ten plant height."}
        class="leaveButton hidden"
        >Sell leaves 100
      </button>
      <p class="text" style="font-size: 1.5em;">Power: {power}</p>
      <div>
        <p class="text" style="font-size: 1.5em;">
          Plant height: {plantHeight.toFixed(2)}
        </p>
      </div>
      <p class="text" style="font-size: 1.5em;">
        Growth per second: {growthPerSecond.toFixed(2)}
      </p>
    </div>
  </div>
</div>
<div class="content">
{#each tasks as task}
  <!-- Tooltip will appear when hovering over the button -->
  <div class="buttonBlock">
    <button
      class="button"
      style="display: block;"
      on:click={function () {
        task.flipSelected();
      }}
      title={task.toolTipText}
    >
      <p>{task.completeions}</p>
      {task.name}
      <div class="outer">
        <div
          class="inside"
          id={task.id}
          style="width: {task.getProgress()}%"
        ></div>
      </div>
    </button>
  </div>
{/each}

<div class="log" id="log">
  <p>
    Log: Started the game <br /> Log: Do not run out of power it will reset you
  </p>
</div>
</div>
<audio id="complete" src="public/696660__ajgrf__wet-plunger-click.wav"></audio>