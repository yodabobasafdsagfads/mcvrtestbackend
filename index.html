import React, { useState, useEffect, useRef } from 'react';
import { DollarSign, Trophy, Play, RotateCcw } from 'lucide-react';

// Backend Server Integration
const API_KEY = 'sk_test_x1y2z3a4b5c6d7e8f9g0h1i2j3k4l5m6';
const SERVER_URL = window.location.origin;

// Make API request
async function apiRequest(endpoint, method = 'GET', data = null) {
  const options = {
    method,
    headers: {
      'Content-Type': 'application/json',
      'X-API-Key': API_KEY
    }
  };
  
  if (data) {
    options.body = JSON.stringify(data);
  }
  
  const response = await fetch(SERVER_URL + endpoint, options);
  return await response.json();
}

const CashRunner3D = () => {
  const canvasRef = useRef(null);
  const [gameState, setGameState] = useState('menu'); // menu, playing, gameOver
  const [score, setScore] = useState(0);
  const [cash, setCash] = useState(0);
  const [leaderboard, setLeaderboard] = useState([]);
  const [playerName, setPlayerName] = useState('');
  const gameRef = useRef(null);

  // Submit game score to backend
  const submitScore = async (name, totalScore, totalCash) => {
    try {
      const result = await apiRequest('/api/game/score', 'POST', {
        player: name,
        score: totalScore
      });
      console.log('Score submitted:', result);
      return result;
    } catch (error) {
      console.error('Error submitting score:', error);
      // Fallback to local leaderboard on error
      const newEntry = { name, score: totalScore, cash: totalCash, rank: leaderboard.length + 1 };
      const updated = [...leaderboard, newEntry].sort((a, b) => b.score - a.score);
      setLeaderboard(updated.slice(0, 10));
    }
  };

  // Get leaderboard from backend
  const fetchLeaderboard = async () => {
    try {
      const result = await apiRequest('/api/game/leaderboard');
      console.log('Leaderboard:', result);
      
      // Transform backend data to match our display format
      if (result && Array.isArray(result)) {
        const formatted = result.map((entry, index) => ({
          name: entry.player || entry.name,
          score: entry.score,
          cash: entry.score, // Assuming score represents cash earned
          rank: index + 1
        }));
        setLeaderboard(formatted);
      }
    } catch (error) {
      console.error('Error fetching leaderboard:', error);
      // Fallback to empty leaderboard on error
      setLeaderboard([]);
    }
  };

  useEffect(() => {
    fetchLeaderboard();
  }, []);

  useEffect(() => {
    if (gameState !== 'playing') return;

    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    canvas.width = 800;
    canvas.height = 600;

    const game = {
      player: { x: 400, y: 500, width: 40, height: 40, speed: 5 },
      coins: [],
      obstacles: [],
      keys: {},
      score: 0,
      cash: 0,
      lastCoinSpawn: 0,
      lastObstacleSpawn: 0,
      animFrame: 0
    };

    gameRef.current = game;

    const handleKeyDown = (e) => {
      game.keys[e.key] = true;
    };

    const handleKeyUp = (e) => {
      game.keys[e.key] = false;
    };

    window.addEventListener('keydown', handleKeyDown);
    window.addEventListener('keyup', handleKeyUp);

    const spawnCoin = () => {
      game.coins.push({
        x: Math.random() * (canvas.width - 30),
        y: -30,
        width: 30,
        height: 30,
        value: Math.random() > 0.8 ? 50 : 10,
        rotation: 0
      });
    };

    const spawnObstacle = () => {
      game.obstacles.push({
        x: Math.random() * (canvas.width - 40),
        y: -40,
        width: 40,
        height: 40,
        speed: 2 + Math.random() * 2
      });
    };

    const checkCollision = (a, b) => {
      return a.x < b.x + b.width &&
             a.x + a.width > b.x &&
             a.y < b.y + b.height &&
             a.y + a.height > b.y;
    };

    const draw3DBox = (ctx, x, y, w, h, color, offset = 5) => {
      // Front face
      ctx.fillStyle = color;
      ctx.fillRect(x, y, w, h);
      
      // Top face (lighter)
      ctx.fillStyle = adjustBrightness(color, 30);
      ctx.beginPath();
      ctx.moveTo(x, y);
      ctx.lineTo(x + offset, y - offset);
      ctx.lineTo(x + w + offset, y - offset);
      ctx.lineTo(x + w, y);
      ctx.closePath();
      ctx.fill();
      
      // Right face (darker)
      ctx.fillStyle = adjustBrightness(color, -30);
      ctx.beginPath();
      ctx.moveTo(x + w, y);
      ctx.lineTo(x + w + offset, y - offset);
      ctx.lineTo(x + w + offset, y + h - offset);
      ctx.lineTo(x + w, y + h);
      ctx.closePath();
      ctx.fill();
    };

    const adjustBrightness = (color, percent) => {
      const num = parseInt(color.replace('#', ''), 16);
      const amt = Math.round(2.55 * percent);
      const R = (num >> 16) + amt;
      const G = (num >> 8 & 0x00FF) + amt;
      const B = (num & 0x0000FF) + amt;
      return '#' + (0x1000000 + (R < 255 ? R < 1 ? 0 : R : 255) * 0x10000 +
        (G < 255 ? G < 1 ? 0 : G : 255) * 0x100 +
        (B < 255 ? B < 1 ? 0 : B : 255))
        .toString(16).slice(1);
    };

    const gameLoop = (timestamp) => {
      ctx.fillStyle = '#1a1a2e';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      // Draw grid
      ctx.strokeStyle = '#16213e';
      ctx.lineWidth = 1;
      for (let i = 0; i < canvas.height; i += 40) {
        ctx.beginPath();
        ctx.moveTo(0, i);
        ctx.lineTo(canvas.width, i);
        ctx.stroke();
      }

      // Move player
      if (game.keys['ArrowLeft'] && game.player.x > 0) {
        game.player.x -= game.player.speed;
      }
      if (game.keys['ArrowRight'] && game.player.x < canvas.width - game.player.width) {
        game.player.x += game.player.speed;
      }

      // Spawn coins
      if (timestamp - game.lastCoinSpawn > 1000) {
        spawnCoin();
        game.lastCoinSpawn = timestamp;
      }

      // Spawn obstacles
      if (timestamp - game.lastObstacleSpawn > 2000) {
        spawnObstacle();
        game.lastObstacleSpawn = timestamp;
      }

      // Update and draw coins
      game.coins = game.coins.filter(coin => {
        coin.y += 3;
        coin.rotation += 0.1;

        if (checkCollision(game.player, coin)) {
          game.score += coin.value;
          game.cash += coin.value;
          setScore(game.score);
          setCash(game.cash);
          return false;
        }

        if (coin.y > canvas.height) return false;

        // Draw 3D coin
        ctx.save();
        ctx.translate(coin.x + coin.width / 2, coin.y + coin.height / 2);
        ctx.rotate(coin.rotation);
        
        const gradient = ctx.createRadialGradient(0, 0, 0, 0, 0, coin.width / 2);
        gradient.addColorStop(0, '#ffd700');
        gradient.addColorStop(0.5, '#ffed4e');
        gradient.addColorStop(1, '#d4af37');
        
        ctx.fillStyle = gradient;
        ctx.beginPath();
        ctx.arc(0, 0, coin.width / 2, 0, Math.PI * 2);
        ctx.fill();
        
        ctx.fillStyle = '#000';
        ctx.font = 'bold 12px Arial';
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.fillText('$', 0, 0);
        
        ctx.restore();

        return true;
      });

      // Update and draw obstacles
      game.obstacles = game.obstacles.filter(obs => {
        obs.y += obs.speed;

        if (checkCollision(game.player, obs)) {
          setGameState('gameOver');
          return false;
        }

        if (obs.y > canvas.height) return false;

        draw3DBox(ctx, obs.x, obs.y, obs.width, obs.height, '#e74c3c', 6);
        return true;
      });

      // Draw player
      draw3DBox(ctx, game.player.x, game.player.y, game.player.width, game.player.height, '#3498db', 8);

      game.animFrame = requestAnimationFrame(gameLoop);
    };

    game.animFrame = requestAnimationFrame(gameLoop);

    return () => {
      window.removeEventListener('keydown', handleKeyDown);
      window.removeEventListener('keyup', handleKeyUp);
      if (game.animFrame) {
        cancelAnimationFrame(game.animFrame);
      }
    };
  }, [gameState]);

  const startGame = () => {
    setScore(0);
    setCash(0);
    setGameState('playing');
  };

  const handleGameOver = async () => {
    if (playerName.trim()) {
      await submitScore(playerName, score, cash);
      await fetchLeaderboard();
    }
    setGameState('menu');
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 text-white p-8">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-8">
          <h1 className="text-5xl font-bold mb-2 bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent">
            Cash Runner 3D
          </h1>
          <p className="text-gray-300">Collect coins, avoid obstacles!</p>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          <div className="lg:col-span-2">
            <div className="bg-slate-800 rounded-lg p-6 shadow-2xl">
              {gameState === 'menu' && (
                <div className="flex flex-col items-center justify-center h-[600px] space-y-6">
                  <DollarSign className="w-24 h-24 text-yellow-400 animate-bounce" />
                  <h2 className="text-3xl font-bold">Ready to Play?</h2>
                  <p className="text-gray-400 text-center max-w-md">
                    Use arrow keys to move left and right. Collect golden coins to earn cash!
                  </p>
                  <button
                    onClick={startGame}
                    className="flex items-center gap-2 px-8 py-4 bg-gradient-to-r from-green-500 to-emerald-600 rounded-lg font-bold text-lg hover:from-green-600 hover:to-emerald-700 transition-all transform hover:scale-105"
                  >
                    <Play className="w-6 h-6" />
                    Start Game
                  </button>
                </div>
              )}

              {gameState === 'playing' && (
                <div>
                  <div className="flex justify-between mb-4">
                    <div className="flex items-center gap-2 bg-slate-900 px-4 py-2 rounded-lg">
                      <Trophy className="w-5 h-5 text-yellow-400" />
                      <span className="font-bold">Score: {score}</span>
                    </div>
                    <div className="flex items-center gap-2 bg-gradient-to-r from-yellow-600 to-orange-600 px-4 py-2 rounded-lg">
                      <DollarSign className="w-5 h-5" />
                      <span className="font-bold">${cash}</span>
                    </div>
                  </div>
                  <canvas
                    ref={canvasRef}
                    className="w-full border-4 border-slate-700 rounded-lg"
                  />
                </div>
              )}

              {gameState === 'gameOver' && (
                <div className="flex flex-col items-center justify-center h-[600px] space-y-6">
                  <h2 className="text-4xl font-bold text-red-400">Game Over!</h2>
                  <div className="text-center space-y-2">
                    <p className="text-2xl">Final Score: {score}</p>
                    <p className="text-3xl font-bold text-yellow-400">Cash Earned: ${cash}</p>
                  </div>
                  <input
                    type="text"
                    placeholder="Enter your name"
                    value={playerName}
                    onChange={(e) => setPlayerName(e.target.value)}
                    className="px-4 py-2 bg-slate-700 rounded-lg text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-yellow-400"
                  />
                  <div className="flex gap-4">
                    <button
                      onClick={handleGameOver}
                      className="flex items-center gap-2 px-6 py-3 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg font-bold hover:from-blue-600 hover:to-purple-700 transition-all"
                    >
                      <RotateCcw className="w-5 h-5" />
                      Back to Menu
                    </button>
                    <button
                      onClick={startGame}
                      className="flex items-center gap-2 px-6 py-3 bg-gradient-to-r from-green-500 to-emerald-600 rounded-lg font-bold hover:from-green-600 hover:to-emerald-700 transition-all"
                    >
                      <Play className="w-5 h-5" />
                      Play Again
                    </button>
                  </div>
                </div>
              )}
            </div>
          </div>

          <div className="lg:col-span-1">
            <div className="bg-slate-800 rounded-lg p-6 shadow-2xl">
              <div className="flex items-center gap-2 mb-6">
                <Trophy className="w-6 h-6 text-yellow-400" />
                <h3 className="text-2xl font-bold">Leaderboard</h3>
              </div>
              <div className="space-y-3">
                {leaderboard.map((entry, index) => (
                  <div
                    key={index}
                    className={`flex items-center justify-between p-4 rounded-lg ${
                      index === 0
                        ? 'bg-gradient-to-r from-yellow-600 to-orange-600'
                        : index === 1
                        ? 'bg-gradient-to-r from-gray-400 to-gray-500'
                        : index === 2
                        ? 'bg-gradient-to-r from-orange-700 to-orange-800'
                        : 'bg-slate-700'
                    }`}
                  >
                    <div className="flex items-center gap-3">
                      <span className="text-2xl font-bold">#{index + 1}</span>
                      <span className="font-semibold">{entry.name}</span>
                    </div>
                    <div className="text-right">
                      <div className="text-lg font-bold">${entry.cash}</div>
                      <div className="text-sm opacity-75">{entry.score} pts</div>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

export default CashRunner3D;
