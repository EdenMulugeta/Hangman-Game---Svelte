<script>
  //   import hangman0 from "/Images/hangman0.png";
  //   import hangman1 from "/Images/hangman1.png";
  //   import hangman2 from "/Images/hangman2.png";
  //   import hangman3 from "/Images/hangman3.png";
  //   import hangman4 from "/Images/hangman4.png";
  //   import hangman5 from "/Images/hangman5.png";
  //   import hangman6 from "/Images/hangman6.png";

  //   //   let images = [
  //   //     { id: 0, path: hangman0 },
  //   //     { id: 1, path: hangman1 },
  //   //     { id: 2, path: hangman2 },
  //   //     { id: 3, path: hangman3 },
  //   //     { id: 4, path: hangman4 },
  //   //     { id: 5, path: hangman5 },
  //   //     { id: 6, path: hangman6 },
  //   //   ];

  //   const images = [
  //     hangman0,
  //     hangman1,
  //     hangman2,
  //     hangman3,
  //     hangman4,
  //     hangman5,
  //     hangman6,
  //   ];
  const wordsWithHints = [
    { word: "ABILITY", hint: "The capacity to do something." },
    { word: "BANANA", hint: "A long yellow fruit." },
    { word: "APPLE", hint: "A common fruit, often red or green." },
    { word: "WATERMELON", hint: "A large green fruit with sweet red flesh." },
    {
      word: "COMPUTER",
      hint: "An electronic device for storing and processing data.",
    },
    {
      word: "OCEAN",
      hint: "A vast body of salt water that covers most of the Earth's surface.",
    },
    {
      word: "MOUNTAIN",
      hint: "A large natural elevation of the Earth's surface.",
    },
    { word: "CELEBRATION", hint: "A joyful occasion for special festivities." },
    { word: "FRIENDSHIP", hint: "A mutual bond between people." },
    { word: "TRIANGLE", hint: "A shape with three sides." },
    {
      word: "TELEPHONE",
      hint: "A device used for communication over distances.",
    },
    {
      word: "HANGMAN",
      hint: "A game where players guess letters to find a hidden word.",
    },
    { word: "LIBRARY", hint: "A place where books are stored for public use." },
    {
      word: "SANDWICH",
      hint: "A food item consisting of filling between two pieces of bread.",
    },
    { word: "GIRAFFE", hint: "A tall animal known for its long neck." },
    { word: "ASTRONOMY", hint: "The study of celestial bodies." },
    {
      word: "SYMPHONY",
      hint: "An elaborate musical composition for orchestra.",
    },
    {
      word: "ELECTRICITY",
      hint: "A form of energy resulting from the flow of electric charge.",
    },
    {
      word: "PHOTOGRAPHY",
      hint: "The art or practice of taking and processing photographs.",
    },
    {
      word: "VIRTUAL",
      hint: "Not physically existing as such but made by software.",
    },
  ];

  let answerArray = [];
  let mistakes = 0;
  let word = "";
  let isGameOver = false;
  let notification = "";
  let currentHint = "";

  function randomWord() {
    const selected =
      wordsWithHints[Math.floor(Math.random() * wordsWithHints.length)];
    word = selected.word;
    currentHint = selected.hint;
    return word;
  }

  function startGame() {
    mistakes = 0;
    word = randomWord();
    answerArray = Array(word.length).fill("___");
    isGameOver = false;
    notification = "";
  }

  function updateHangmanPicture() {
    return `/Images/hangman${mistakes}.png`;
  }

  function handleGuess(guess) {
    let found = false;
    for (let i = 0; i < word.length; i++) {
      if (word[i] === guess) {
        answerArray[i] = guess;
        found = true;
      }
    }
    if (!found) {
      mistakes += 1;
    }

    checkVictory();
  }

  function checkVictory() {
    if (answerArray.join("") === word) {
      notification = "You won!";
      isGameOver = true;
    }
    if (mistakes === 6) {
      notification = "You lost!";
      isGameOver = true;
    }
  }

  function showHint() {
    alert(currentHint);
  }

  startGame();
</script>

<div class="wrapper">
  <h1>Hangman Game</h1>
  <h3>Mistakes: {mistakes} out of 6</h3>
  <img
    class="hangman"
    src="/Images/hangman{mistakes}.png"
    alt="Hangman Image"
  />
  <div class="word-div">{answerArray.join(" ")}</div>

  <button class="hint-button" on:click={showHint} disabled={isGameOver}>
    Get a Hint
  </button>

  <div id="buttons">
    {#each "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("") as letter}
      <button
        class="button"
        on:click={() => handleGuess(letter)}
        disabled={isGameOver}
      >
        {letter}
      </button>
    {/each}
  </div>

  {#if notification}
    <div class="notification">
      <h3>{notification}</h3>
      <h4>Correct Word: {word}</h4>
      <button class="notif-btn" on:click={startGame}>Play again</button>
    </div>
  {/if}
</div>

<style>
  :global(body) {
    background-image: url("/Images/gamebackgound.png");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: fixed;
  }

  h3 {
    padding-right: 20px;
    font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    font-size: xx-large;
    font-weight: 900;
  }
  .hint-button {
    margin: 20px;
    font-size: 20px;
    background: #ffe5b4;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    padding: 10px;
  }

  .hint-button:hover {
    background-color: #e75480;
  }
  .notif-btn {
    font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    font-size: large;
    font-weight: 900;
  }
  .reset {
    padding-left: 950px;
    padding-top: 50px;
  }
  .reset-btn {
    width: 50px;
    height: 50px;
    background: #ffe5b4;
    border: none;
    border-radius: 4px;
    margin: 3px;
  }
  /*   .alpha {
    width: 60px;
    height: 30px;
    background: #ffe5b4;
    border: none;
    border-radius: 4px;
    margin: 3px;
    
  }
  .alpha:hover {
    background-color: #e75480;
    
  } */
  .disabled {
    background-color: darkgray;
  }

  .word-div {
    font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    font-size: xx-large;
    font-weight: 900;
    display: inline-flex;
    padding-top: 200px;
    padding-left: 300px;
    margin: 80px;
  }
  .word {
    margin-right: 1.5rem;
    width: 50px;
    height: 30px;
    background: #fff;
    border: none;
    border-radius: 4px;
    margin: 3px;
  }
  .button {
    font-size: 30px;
    width: 80px;
    height: 60px;
    background: #ffe5b4;
    border: none;
    border-radius: 4px;
    margin: 3px;
  }
  .button:hover {
    background-color: #e75480;
  }
  .notif {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: rgb(36, 167, 167);
    width: 20rem;
    padding: 20px 10px;
    border-radius: 4px;
    box-shadow: 3px 3px 1px 1px rgba(0, 0, 0, 0.2);
  }

  .notif-hidden {
    display: none;
  }
  .hidden {
    display: none;
  }

  .hangman {
    float: left;
    padding-top: 100px;
    height: 500px;
    width: 500px;
  }
</style>
