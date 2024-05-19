<head>
  <style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f0f8ff;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        margin: 0;
    }
    #output, #score, #result, #points {
        margin: 10px;
        padding: 10px;
        border-radius: 5px;
        background-color: #ffffff;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 80%;
        max-width: 600px;
        text-align: center;
    }
    button {
        font-size: 1.2em;
        padding: 10px 20px;
        margin: 10px;
        border: none;
        border-radius: 5px;
        background-color: #4CAF50;
        color: white;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    button:hover {
        background-color: #45a049;
    }
    button:disabled {
        background-color: #cccccc;
        cursor: not-allowed;
    }
    #play_again {
        background-color: #f44336;
    }
    #play_again:hover {
        background-color: #e53935;
    }

    .game-info {
            font-size: 1.1em;
            font-weight: bold;
            color: #333;
        }

   .game-infoUserWin {
            font-size: 1.1em;
            font-weight: bold;
            color: #328621;
        }

    .game-infoCompWin {
            font-size: 1.1em;
            font-weight: bold;
            color: #bb1611;
        }

    .game-userFont {
            font-size: 1.1em;
            font-weight: bold;
            color: #110c0b;
        }
</style>

</head>

  <title>MyGame - Rock,Paper or Scissors</title>
    <h1>Rock, Paper or Scissors?</h1>
    <body> 
  
      <button id="button_rock" onclick="playGame('rock')">Rock</button>
      <button id="button_scissors" onclick="playGame('scissors')">Scissors</button>
      <button id="button_paper" onclick="playGame('paper')">Paper</button>
      <button id="play_again" onclick="resetGame()">Play Again</button>
      <div id="output"></div>
      <p id="points"></p>   
      <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.3.3/dist/confetti.browser.min.js"></script>
      
      <!--för att spelet skulle se lite trevligare ut så googlade jag fram lite färdiga lösningar på utseende saker, som tex font och konfetti och stil på sidan.-->
    
    <script>

/* HEJ TOBIAS, DETTA ÄR MITT TANKESCHEMA SOM JAG GICK EFTER NÄR JAG SKAPADE SPELET.
   

   1. Genom att trycka på en knapp så ska spelet köras.(X)
   2. Datorn ska slumpmässigt välja ett tal som ska genera sten, sax eller påse.(X)
   3. Programmet ska nu avgöra en vinnare genom 3 olika villkor, vinnare, förlorare eller oavgjort (X)
   4. Programmet ska skriva ut vad jag valde, vad datorn valde och vem som vann(X)
   5. sedan ska programmet addera 5 poäng till vinnaren(X)
   6. När programmet körs igen, ska poängen kommas ihåg samt att den gamla datan ska förvinna(X)
   7. När max poäng på 15 har uppnåtts så ska det inte vara möjligt att fortsätta samma spel (X)
   8. En vinnare ska utses automatiskt om man kommer upp till 15 poäng(X)
   9. Konfetti kod ska köras när 15 poäng uppnåtts.(X)
*/


// PROGRAMMET //


    let point_user = 0;
    let point_comp = 0;

  
  let getComputerChoice = () => {
    const randomNumber = Math.floor(Math.random() * 3 + 1);
  
    switch(randomNumber) {
    case 1:
    return 'rock'
    break;
    case 2:
    return 'paper'
    break;
    case 3:
    return 'scissors'
    break;
    default: 'error with computer choice'
    break;
    }    
  }


  let determineWinner = (userChoice, computerChoice) => {
    
    
    if(userChoice === computerChoice){
      const message_tie = print(`<span class="game-userFont">This Round Is A Draw!</span>`);
      return(message_tie);
      }

    if(userChoice === 'rock'){
      if(computerChoice === 'scissors'){  
        const message_user = print(`<span class="game-infoUserWin">You Won this round</span>`);
        return [message_user, point_user +=5];
      } else { 
        const message_comp = print(`<span class="game-infoCompWin">The Computer Won this round</span>`);
        return [message_comp, point_comp +=5];
      }
    }

    if(userChoice === 'paper'){
      if(computerChoice === 'rock'){
        const message_user = print(`<span class="game-infoUserWin">You Won this round</span>`);
        return [message_user, point_user +=5];
        
      } else {
        const message_comp = print(`<span class="game-infoCompWin">The Computer Won this round</span>`);
        return [message_comp, point_comp +=5];
      }
    }

    if(userChoice === 'scissors'){
      if(computerChoice === 'paper'){       
        const message_user = print(`<span class="game-infoUserWin">You Won this round</span>`);
        return [message_user, point_user +=5];       
      } else {
        const message_comp = print(`<span class="game-infoCompWin">The Computer Won this round</span>`);
        return [message_comp, point_comp +=5];
      }              
    }
}

 

  const playGame = (userChoice) => {
  let computerChoice = getComputerChoice();
    clearOutPut();
    print(`<span class="game-userFont">User Choice: </span>`);
    newLine();
    newLine();
    print(userChoice);
    newLine();
    newLine();
    newLine();
    print(`<span class="game-userFont">Computer Choice: </span`);
    newLine();
    newLine();
    print(computerChoice);
    newLine();
    newLine();
    newLine();
    newLine();
    determineWinner(userChoice, computerChoice);
    newLine();
    newLine();
    updateScore();

    if(point_user >= 15 || point_comp >= 15){
      triggerConfetti();
      print(`<span class="game-info">The Game Has Ended</span>`);
      disableButtons();
    } else {
      print('');
    }
    
  } 

 



  // FUNKTIONER //
  
  

  function print(text){
    document.getElementById("output").innerHTML += text;
  }

  function printScore() {
    document.getElementById("score").innerHTML += text;
  }
  

  function newLine(){
    document.getElementById("output").innerHTML += "<br>";
  }
  

  function clearOutPut(){
    document.getElementById("output").innerHTML = "";
  }   
  
  function updateScore() {
    document.getElementById("points").innerHTML = "Points: User " + point_user + " - Computer " + point_comp;
  }

  function disableButtons() {
    document.getElementById("button_rock").disabled = true;
    document.getElementById("button_scissors").disabled = true;
    document.getElementById("button_paper").disabled = true;
 }

function enableButtons() {
    document.getElementById("button_rock").disabled = false;
    document.getElementById("button_scissors").disabled = false;
    document.getElementById("button_paper").disabled = false;
 }

 function resetGame() {  
    point_user = 0;
    point_comp = 0;   
    updateScore();
    enableButtons();
    document.getElementById("output").innerHTML = "";
 }

 function triggerConfetti() {
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });
        }

      </script>
    </body>
  </head>
