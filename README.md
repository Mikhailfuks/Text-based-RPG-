const player = {
  name: "",
  health: 100,
  attack: 10,
  defense: 5,
  inventory: [],
  gold: 0
};

const enemies = [
  { name: "Goblin", health: 20, attack: 5, defense: 2 },
  { name: "Wolf", health: 30, attack: 8, defense: 3 },
  { name: "Ogre", health: 50, attack: 15, defense: 8 }
];

let currentRoom = {
  description: "You stand at the entrance to a dark forest.",
  exits: ["north"]
};

function startGame() {
  player.name = prompt("What is your name, adventurer?");
  console.log(Welcome, ${player.name}!);
  showRoom();
}

function showRoom() {
  console.log(currentRoom.description);
  console.log("Exits:", currentRoom.exits.join(", "));

  const action = prompt("What do you want to do? (e.g. 'go north', 'attack goblin', 'look around')").toLowerCase();
  handleAction(action);
}

function handleAction(action) {
  const words = action.split(" ");

  if (words[0] === "go") {
    handleGo(words[1]);
  } else if (words[0] === "attack") {
    handleAttack(words[1]);
  } else if (words[0] === "look") {
    handleLook();
  } else {
    console.log("Invalid action.");
    showRoom();
  }
}

function handleGo(direction) {
  if (currentRoom.exits.includes(direction)) {
    // Move to a new room based on your game's logic (use an array of room objects)
    // For now, let's just print a message
    console.log(You go ${direction}.);
    // update currentRoom to a new room object
    showRoom();
  } else {
    console.log("You can't go that way.");
    showRoom();
  }
}

function handleAttack(enemyName) {
  const enemy = enemies.find(e => e.name.toLowerCase() === enemyName.toLowerCase());

  if (enemy) {
    // Implement combat logic
    // Example:
    let playerDamage = player.attack - enemy.defense;
    let enemyDamage = enemy.attack - player.defense;
    enemy.health -= playerDamage;
    player.health -= enemyDamage;

    console.log(You attack the ${enemy.name} for ${playerDamage} damage.);
    console.log(The ${enemy.name} attacks you for ${enemyDamage} damage.);

    if (enemy.health <= 0) {
      console.log(You have defeated the ${enemy.name}!);
      // Award gold, experience, or loot
    } else if (player.health <= 0) {
      console.log("You have been defeated!");
      // Game over
    } else {
      showRoom(); // Continue the combat loop
    }
  } else {
    console.log("There is no " + enemyName + " here.");
    showRoom();
  }
}

function handleLook() {
  // Implement logic to describe the current room in more detail, possibly with a random event
  console.log("You look around...");
  // Example:
  if (Math.random() < 0.2) {
    console.log("You find a shiny gold coin on the ground!");
    player.gold++;
  }
  showRoom();
}

startGame();
