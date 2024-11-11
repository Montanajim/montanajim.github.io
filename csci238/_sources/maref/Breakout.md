# Breakout



```dart
import 'package:flutter/material.dart';
import 'dart:async';

void main() => runApp(BrickBreakoutGame());

class BrickBreakoutGame extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        backgroundColor: Colors.black,
        body: GameScreen(),
      ),
    );
  }
}

class GameScreen extends StatefulWidget {
  @override
  _GameScreenState createState() => _GameScreenState();
}

class _GameScreenState extends State<GameScreen> {
  // Ball position and speed
  double ballX = 0.0;
  double ballY = 0.0;
  double ballSpeedX = 0.02;
  double ballSpeedY = 0.02;

  // Paddle position
  double paddleX = 0.0;
  double paddleWidth = 0.4;

  // Brick variables
  int numRows = 3;
  int numCols = 5;
  List<List<bool>> bricks = [];

  @override
  void initState() {
    super.initState();
    _initializeBricks();
    _startGame();
  }

  void _initializeBricks() {
    for (int i = 0; i < numRows; i++) {
      bricks.add(List.filled(numCols, true));
    }
  }

  void _startGame() {
    Timer.periodic(Duration(milliseconds: 30), (timer) {
      setState(() {
        _moveBall();
      });
    });
  }

  void _moveBall() {
    ballX += ballSpeedX;
    ballY += ballSpeedY;

    // Ball collision with walls
    if (ballX <= -1 || ballX >= 1) ballSpeedX = -ballSpeedX;
    if (ballY <= -1) ballSpeedY = -ballSpeedY;

    // Ball collision with paddle
    if (ballY >= 0.9 &&
        ballX >= paddleX - paddleWidth / 2 &&
        ballX <= paddleX + paddleWidth / 2) {
      ballSpeedY = -ballSpeedY;
    }

    // Ball collision with bricks
    for (int i = 0; i < numRows; i++) {
      for (int j = 0; j < numCols; j++) {
        if (bricks[i][j]) {
          double brickTop = -0.8 + i * 0.2;
          double brickLeft = -1 + j * 0.4;
          double brickRight = brickLeft + 0.4;

          if (ballY >= brickTop &&
              ballY <= brickTop + 0.1 &&
              ballX >= brickLeft &&
              ballX <= brickRight) {
            bricks[i][j] = false;
            ballSpeedY = -ballSpeedY;
          }
        }
      }
    }

    // Ball out of bounds (Game Over)
    if (ballY >= 1) {
      _resetGame();
    }
  }

  void _resetGame() {
    ballX = 0.0;
    ballY = 0.0;
    ballSpeedX = 0.02;
    ballSpeedY = 0.02;
    paddleX = 0.0;
    bricks.clear();
    _initializeBricks();
  }

  void _movePaddle(DragUpdateDetails details) {
    setState(() {
      paddleX += details.delta.dx / MediaQuery.of(context).size.width * 2;
      paddleX = paddleX.clamp(-1 + paddleWidth / 2, 1 - paddleWidth / 2);
    });
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onHorizontalDragUpdate: _movePaddle,
      child: Stack(
        children: [
          // Ball
          Align(
            alignment: Alignment(ballX, ballY),
            child: Container(
              width: 20,
              height: 20,
              decoration: BoxDecoration(
                color: Colors.white,
                shape: BoxShape.circle,
              ),
            ),
          ),
          // Paddle
          Align(
            alignment: Alignment(paddleX, 0.95),
            child: Container(
              width: MediaQuery.of(context).size.width * paddleWidth,
              height: 20,
              color: Colors.blue,
            ),
          ),
          // Bricks
          for (int i = 0; i < numRows; i++)
            for (int j = 0; j < numCols; j++)
              if (bricks[i][j])
                Align(
                  alignment: Alignment(-1 + j * 0.4 + 0.2, -0.8 + i * 0.2),
                  child: Container(
                    width: MediaQuery.of(context).size.width * 0.2,
                    height: 40,
                    color: Colors.red,
                  ),
                ),
        ],
      ),
    );
  }
}

```

