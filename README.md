<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tikki Topple - 1 vs 4 Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            max-width: 900px;
            width: 100%;
            padding: 30px;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 2.5em;
        }

        .game-board {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            margin-bottom: 30px;
        }

        .tile {
            aspect-ratio: 1;
            border: 3px solid #ccc;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            user-select: none;
            position: relative;
            overflow: hidden;
        }

        .tile:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .tile.player-1 {
            background: linear-gradient(135deg, #FF6B6B 0%, #FF8E72 100%);
            color: white;
            border-color: #FF6B6B;
        }

        .tile.player-2 {
            background: linear-gradient(135deg, #4ECDC4 0%, #44A08D 100%);
            color: white;
            border-color: #4ECDC4;
        }

        .tile.player-3 {
            background: linear-gradient(135deg, #FFE66D 0%, #FFA502 100%);
            color: white;
            border-color: #FFE66D;
        }

        .tile.player-4 {
            background: linear-gradient(135deg, #95E1D3 0%, #38ADA9 100%);
            color: white;
            border-color: #95E1D3;
        }

        .tile.player-5 {
            background: linear-gradient(135deg, #A8E6CF 0%, #56AB2F 100%);
            color: white;
            border-color: #A8E6CF;
        }

        .tile.empty {
            background: #f5f5f5;
            color: #999;
            cursor: not-allowed;
        }

        .tile.fallen {
            animation: topple 0.6s ease-in-out;
            transform: rotateZ(45deg) translateY(50px);
            opacity: 0.3;
        }

        @keyframes topple {
            0% {
                transform: rotateZ(0deg) translateY(0);
                opacity: 1;
            }
            50% {
                transform: rotateZ(25deg) translateY(25px);
            }
            100% {
                transform: rotateZ(45deg) translateY(50px);
                opacity: 0.3;
            }
        }

        .info-section {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-bottom: 20px;
        }

        .info-box {
            padding: 15px;
            border-radius: 10px;
            background: #f9f9f9;
            border-left: 5px solid #667eea;
        }

        .info-box h3 {
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .current-player {
            font-size: 1.5em;
            font-weight: bold;
            color: #333;
        }

        .scores {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .score-card {
            padding: 10px;
            border-radius: 8px;
            text-align: center;
            color: white;
            font-weight: bold;
        }

        .score-card.player-1 {
            background: #FF6B6B;
        }

        .score-card.player-2 {
            background: #4ECDC4;
        }

        .score-card.player-3 {
            background: #FFE66D;
            color: #333;
        }

        .score-card.player-4 {
            background: #95E1D3;
            color: #333;
        }

        .score-card.player-5 {
            background: #A8E6CF;
            color: #333;
        }

        .score-card p:first-child {
            font-size: 0.9em;
            opacity: 0.9;
        }

        .score-card p:last-child {
            font-size: 1.8em;
            margin-top: 5px;
        }

        .controls {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        button {
            padding: 12px 30px;
            font-size: 1em;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #e0e0e0;
            color: #333;
        }

        .btn-secondary:hover {
            background: #d0d0d0;
        }

        .game-status {
            text-align: center;
            font-size: 1.2em;
            font-weight: bold;
            margin-top: 20px;
            min-height: 30px;
        }

        .winner-message {
            color: #28a745;
            font-size: 1.5em;
            animation: pulse 0.5s ease-in-out;
        }

        .loser-message {
            color: #dc3545;
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.1);
            }
        }

        .rules {
            margin-top: 30px;
            padding: 20px;
            background: #f0f0f0;
            border-radius: 10px;
            border-left: 5px solid #667eea;
        }

        .rules h3 {
            margin-bottom: 10px;
            color: #333;
        }

        .rules ul {
            list-style: none;
            color: #666;
            font-size: 0.95em;
        }

        .rules li {
            padding: 5px 0;
            padding-left: 25px;
            position: relative;
        }

        .rules li:before {
            content: "▸";
            position: absolute;
            left: 0;
            color: #667eea;
        }

        @media (max-width: 600px) {
            .info-section {
                grid-template-columns: 1fr;
            }

            .game-board {
                grid-template-columns: repeat(2, 1fr);
            }

            h1 {
                font-size: 1.8em;
            }

            .scores {
                grid-template-columns: repeat(3, 1fr);
                gap: 5px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎮 Tikki Topple</h1>

        <div class="info-section">
            <div class="info-box">
                <h3>Current Player:</h3>
                <div class="current-player" id="currentPlayer">Player 1</div>
            </div>
            <div class="info-box">
                <h3>Remaining Tiles:</h3>
                <div class="current-player" id="remainingTiles">16</div>
            </div>
        </div>

        <h3 style="text-align: center; margin-bottom: 15px;">Scores</h3>
        <div class="scores" id="scoresContainer"></div>

        <h3 style="text-align: center; margin: 20px 0 15px 0;">Game Board</h3>
        <div class="game-board" id="gameBoard"></div>

        <div class="controls">
            <button class="btn-primary" id="resetBtn">New Game</button>
            <button class="btn-secondary" id="undoBtn">Undo Last Move</button>
        </div>

        <div class="game-status" id="gameStatus"></div>

        <div class="rules">
            <h3>How to Play</h3>
            <ul>
                <li><strong>1 Player</strong> (Red) vs <strong>4 AI Players</strong> (Cyan, Yellow, Teal, Green)</li>
                <li>Players take turns clicking on tiles</li>
                <li>When you click a tile, it "topples" and that player claims it</li>
                <li>The last player to have a tile standing wins!</li>
                <li>Strategy: Try to force opponents to run out of tiles first</li>
                <li>Use <strong>Undo</strong> to take back your last move</li>
            </ul>
        </div>
    </div>

    <script>
        class TikkiToppleGame {
            constructor() {
                this.players = [
                    { id: 1, name: 'Player 1', color: 'player-1', isAI: false },
                    { id: 2, name: 'Player 2', color: 'player-2', isAI: true },
                    { id: 3, name: 'Player 3', color: 'player-3', isAI: true },
                    { id: 4, name: 'Player 4', color: 'player-4', isAI: true },
                    { id: 5, name: 'Player 5', color: 'player-5', isAI: true }
                ];
                
                this.boardSize = 16;
                this.tiles = [];
                this.currentPlayerIndex = 0;
                this.scores = {};
                this.gameOver = false;
                this.history = [];
                
                this.initializeGame();
                this.setupEventListeners();
                this.render();
            }

            initializeGame() {
                this.tiles = Array(this.boardSize).fill(null);
                this.scores = {};
                this.players.forEach(player => {
                    this.scores[player.id] = 0;
                });
                this.currentPlayerIndex = 0;
                this.gameOver = false;
                this.history = [];
            }

            setupEventListeners() {
                document.getElementById('gameBoard').addEventListener('click', (e) => {
                    if (e.target.classList.contains('tile') && !this.players[this.currentPlayerIndex].isAI) {
                        const index = Array.from(document.querySelectorAll('.tile')).indexOf(e.target);
                        this.playMove(index);
                    }
                });

                document.getElementById('resetBtn').addEventListener('click', () => this.reset());
                document.getElementById('undoBtn').addEventListener('click', () => this.undo());
            }

            playMove(index) {
                if (this.gameOver || this.tiles[index] !== null) return;

                // Save state for undo
                this.history.push({
                    tiles: [...this.tiles],
                    currentPlayerIndex: this.currentPlayerIndex,
                    scores: {...this.scores}
                });

                // Place tile
                this.tiles[index] = this.players[this.currentPlayerIndex].id;
                this.scores[this.players[this.currentPlayerIndex].id]++;

                // Check for game over
                if (this.isBoardFull()) {
                    this.gameOver = true;
                    this.determineWinner();
                } else {
                    this.nextTurn();
                }

                this.render();

                // AI move after a delay
                if (!this.gameOver && this.players[this.currentPlayerIndex].isAI) {
                    setTimeout(() => this.aiMove(), 800);
                }
            }

            aiMove() {
                if (this.gameOver) return;

                const emptyTiles = this.tiles
                    .map((tile, index) => tile === null ? index : null)
                    .filter(index => index !== null);

                if (emptyTiles.length > 0) {
                    // Simple AI: pick a random empty tile
                    const randomIndex = emptyTiles[Math.floor(Math.random() * emptyTiles.length)];
                    this.playMove(randomIndex);
                }
            }

            nextTurn() {
                this.currentPlayerIndex = (this.currentPlayerIndex + 1) % this.players.length;
            }

            isBoardFull() {
                return this.tiles.every(tile => tile !== null);
            }

            determineWinner() {
                const playerWithMostTiles = Object.keys(this.scores).reduce((prev, current) =>
                    this.scores[current] > this.scores[prev] ? current : prev
                );

                const winnerName = this.players.find(p => p.id == playerWithMostTiles).name;
                const winnerMessage = playerWithMostTiles == 1 
                    ? `🎉 ${winnerName} WINS! 🎉` 
                    : `${winnerName} wins`;
                
                document.getElementById('gameStatus').innerHTML = `
                    <span class="${playerWithMostTiles == 1 ? 'winner-message' : 'loser-message'}">
                        ${winnerMessage}
                    </span>
                `;
            }

            undo() {
                if (this.history.length === 0 || this.gameOver) return;

                const previousState = this.history.pop();
                this.tiles = previousState.tiles;
                this.currentPlayerIndex = previousState.currentPlayerIndex;
                this.scores = previousState.scores;
                document.getElementById('gameStatus').textContent = '';

                this.render();
            }

            reset() {
                this.initializeGame();
                document.getElementById('gameStatus').textContent = '';
                this.render();
            }

            render() {
                this.renderBoard();
                this.renderScores();
                this.updateCurrentPlayer();
                this.updateRemainingTiles();
            }

            renderBoard() {
                const boardContainer = document.getElementById('gameBoard');
                boardContainer.innerHTML = '';

                this.tiles.forEach((playerId, index) => {
                    const tile = document.createElement('div');
                    tile.className = 'tile';

                    if (playerId === null) {
                        tile.classList.add('empty');
                        tile.textContent = '';
                    } else {
                        const player = this.players.find(p => p.id === playerId);
                        tile.classList.add(player.color);
                        tile.classList.add('fallen');
                        tile.textContent = player.id;
                    }

                    boardContainer.appendChild(tile);
                });
            }

            renderScores() {
                const scoresContainer = document.getElementById('scoresContainer');
                scoresContainer.innerHTML = '';

                this.players.forEach(player => {
                    const scoreCard = document.createElement('div');
                    scoreCard.className = `score-card ${player.color}`;
                    scoreCard.innerHTML = `
                        <p>${player.name}</p>
                        <p>${this.scores[player.id]}</p>
                    `;
                    scoresContainer.appendChild(scoreCard);
                });
            }

            updateCurrentPlayer() {
                const currentPlayer = this.players[this.currentPlayerIndex];
                document.getElementById('currentPlayer').textContent = currentPlayer.name;
                document.getElementById('currentPlayer').style.color = 
                    currentPlayer.id === 1 ? '#FF6B6B' : '#333';
            }

            updateRemainingTiles() {
                const remaining = this.tiles.filter(tile => tile === null).length;
                document.getElementById('remainingTiles').textContent = remaining;
            }
        }

        // Initialize game when page loads
        let game;
        window.addEventListener('DOMContentLoaded', () => {
            game = new TikkiToppleGame();
        });
    </script>
</body>
</html>
