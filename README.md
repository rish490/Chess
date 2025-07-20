Chess Game – Object-Oriented Design in C++
📝 Problem Overview
Design and implement a modular, extensible, terminal-based Chess game in C++ using Object-Oriented Programming (OOP) principles. The system should allow two players to play against each other, handle all standard rules of chess (including en passant, check, and checkmate), and support extensibility for future additions like AI or multiplayer.

Key functional goals:

Represent an 8x8 chess board with all standard pieces.

Allow two players to take alternate turns.

Validate legal moves according to the rules of chess.

Detect game-ending conditions (checkmate, stalemate, draw).

Handle special moves like en passant and castling.

Be easily extensible for AI or GUI integration.

💡 Solution Overview
The solution is modeled using object-oriented best practices like abstraction, encapsulation, and separation of concerns. Core design choices:

🔧 Class Structure:
GameContext: Controls overall flow, manages whose turn it is, and triggers move execution.

Board: Owns an 8x8 matrix of piece pointers. Responsible for move validation, move execution, and special rules (e.g., en passant).

Player: Encapsulates player behavior. Delegates move generation to its strategy.

PlayerStrategy (Interface):

HumanStrategy: Takes input from terminal.

AIStrategy: Future extension for AI integration.

Piece (Abstract):

Parent of all piece types like Pawn, Knight, etc.

Provides the movement pattern but not full validation.

GameState: Enum defining states like VALID_MOVE, INVALID_MOVE, CHECK, CHECKMATE, STALEMATE.

✅ Design Improvement: Move Validation Responsibility
Initially, the design considered adding isValidMove(...) logic directly within each piece class. While this might seem intuitive, it mixes move generation and context-dependent validation, violating the Single Responsibility Principle.

Improvement Made:

Each Piece now only describes how it can move (movement rules like L-shape, diagonal, straight, etc.).

The Board class is solely responsible for validating whether a move is legal, considering:

Obstructions

Check/checkmate conditions

En passant

Board boundaries

Turn correctness

This centralization of validation logic avoids duplication, ensures consistent rule enforcement, and makes handling special conditions like check detection much easier.

