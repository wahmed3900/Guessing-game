
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

let min = 1;
let max = 100;
let maxAttempts = 10;
let attempts = 0;
let secretNumber = 0;

function setDifficulty() {
  console.log('Select difficulty level:');
  console.log('1) Easy (1-50, 15 attempts)');
  console.log('2) Medium (1-100, 10 attempts)');
  console.log('3) Hard (1-200, 5 attempts)');

  rl.question('Choose difficulty (1/2/3): ', (answer) => {
    switch (answer.trim()) {
      case '1':
        min = 1;
        max = 50;
        maxAttempts = 15;
        break;
      case '2':
        min = 1;
        max = 100;
        maxAttempts = 10;
        break;
      case '3':
        min = 1;
        max = 200;
        maxAttempts = 5;
        break;
      default:
        console.log('Invalid choice. Defaulting to Medium (1-100, 10 attempts).');
        min = 1;
        max = 100;
        maxAttempts = 10;
    }

    startGame();
  });
}

function startGame() {
  attempts = 0;
  secretNumber = Math.floor(Math.random() * (max - min + 1)) + min;

  console.log(`\nI'm thinking of a number between ${min} and ${max}.`);
  console.log(`You have ${maxAttempts} attempts.\n`);
  askGuess();
}

function askGuess() {
  rl.question(`Enter your guess (${min} - ${max}): `, (answer) => {
    const guess = parseInt(answer, 10);

    if (isNaN(guess) || guess < min || guess > max) {
      console.log(`Please enter a valid number between ${min} and ${max}.`);
      askGuess();
      return;
    }

    attempts += 1;

    if (guess === secretNumber) {
      console.log(`Congratulations! You've guessed the number in ${attempts} attempts!`);
      playAgain();
    } else if (attempts >= maxAttempts) {
      console.log(`Sorry, you've used all your attempts. The number was ${secretNumber}.`);
      playAgain();
    } else {
      console.log(guess < secretNumber ? 'Too low! Try again.' : 'Too high! Try again.');
      askGuess();
    }
  });
}
else {
    console hint = guess <secretNumber ? 'Too low! Try again.' : 'Too high! Try again.';
    console.log(`Wrong guess! ${hint}`);
    askGuest();
}
function playagain() {
    rl.question('Do you want to play again? (yes/no): ', (answer) => {
        if (answer.toLowerCase() === 'yes') {   
            setdDifficulty();
        } else {
            console.log('Thanks for playing! Goodbye!');
            rl.close();
        }   }); 
}

console.log('Welcome to the Number Guessing Game!');
setDifficulty();
