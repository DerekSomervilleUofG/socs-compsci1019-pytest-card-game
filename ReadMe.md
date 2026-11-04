# Introduction

The application plays cards with a standard 52 card deck, with suits hearts, spades, diamonds and clubs. The following two games are played:

* Snap [https://en.m.wikipedia.org/wiki/Snap_(card_game)](https://en.m.wikipedia.org/wiki/Snap_(card_game))
* Twenty One [https://en.wikipedia.org/wiki/Blackjack](https://en.wikipedia.org/wiki/Blackjack) and [Example Twenty One](https://www.youtube.com/watch?v=zuZqw12MrVI)


Unit Testing allows you to test the `CardGame` application completely. For this task, you are required to implement several unit tests using the module `pytest`.

# Instructions

- Fork this project and make sure your repository is public. Then import the project into your IDE VSCode.
- You cannot change the signature of the provided functions or rename them.
- You cannot interact with your peers: work individually and do your best.
- The unit tests to implement are described through a set of sub-tasks.
- Implement the unit tests one at a time, strictly following the order given by the sub-tasks. Do not read ahead to the following sub-tasks. 
- A sub-task can be considered complete once you are confident that the unit test has been implemented correctly.
- Every time you complete a sub-task, commit and push your code.
- At the end of the assignment, make sure you have pushed the entire project to the public repository.

# Sub-tasks

Remember to read and implement the sub-tasks one at a time, following the given order. Do not move on to the next sub-task until the current one has been completed. Implement the required unit tests by working in the `test/test_mock_ConsoleInOut.py`, `test/test_mock_Game.py`, `test/test_mock_LoadCSV.py` & `test/test_mock_Deck.py` files. 

## Sub-task 1 – Test Scoring Hand in TwentyOne

To verify the hand scoring logic in `TwentyOne.py`, including ace adjustment and bust detection.

### Requirement

- Implement unit tests for `score_hand` in `test/test_twenty_one.py`.
- Verify the following test scenarios:
  1. **Standard hand**: A hand without aces calculates the exact sum of card values (e.g., 8 + 10 = 18).
  2. **Ace as high value (11)**: A hand with an ace where the total does not exceed 21 retains the higher ace value (e.g., Ace + 9 = 20).
  3. **Ace adjusted to low value (1)**: When total score exceeds 21, the ace score is reduced to prevent busting (e.g., Ace + 9 + 5 = 15).
  4. **Bust hand**: When the score exceeds 21 (even after ace adjustment, or with no ace), the returned score must be `0`.
- Mock or stub `get_card_score`, `get_face_card_score`, and `ace` where appropriate to isolate the logic of `score_hand`.
- Push sub task to GitHub, [Go To GitHub Commit](#github-commit)

# Sub-task 2 – Verify Exception on Non-Existent File

To verify exception handling when attempting to read an invalid file.

### Requirement

- Implement unit test `test_create_csv_reader_invalid_path` in `test/test_load_csv.py`.
- Call `create_csv_reader` with an invalid or non-existent file path (e.g., `"does_not_exist.csv"`).
- Use `pytest.raises(IOError)` to verify that an `IOError` is properly re-raised.
- Use `capsys` to assert that `"An error occurred."` is printed to stdout.
- Push sub task to GitHub, [Go To GitHub Commit](#github-commit)

## Sub-task 3 – Test Parametrized Hand Scoring with Edge Cases

To verify multiple card combinations and edge cases efficiently in `score_hand` using `@pytest.mark.parametrize`.

### Requirement

- Implement `test_score_hand_combinations` in `test/test_twenty_one.py`.
- Use `@pytest.mark.parametrize` to run a table of test cases against `score_hand`:
  1. Empty hand (score = 0).
  2. Natural 21 (Blackjack: Ace + 10-value card = 21).
  3. Hand exceeding 21 even after reducing Ace to 1 (e.g., Ace + 10 + 10 + 2 = 23 -> busts to 0).
  4. Multiple Aces in hand (e.g., Ace + Ace + 9 = 21).
  5. Exact 21 with multiple low cards (e.g., 7 + 7 + 7 = 21).
- Assert the expected return value for each tuple in the dataset.
- Push sub task to GitHub, [Go To GitHub Commit](#github-commit)

## Sub-task 4 – Test Player Routing in Round Execution

To verify conditional dispatching in `play_a_round` based on competitor type.

### Requirement

- Implement `test_play_a_round_dispatches_by_player_type` in `test/test_twenty_one.py`.
- Configure the global or module-level `players` list with two mock players:
  - One with `COMPETITOR_TYPE = USER`.
  - One with `COMPETITOR_TYPE = COMPUTER` (or any non-USER identifier).
- Mock both `user_plays` and `computer_plays` using `unittest.mock.Mock`.
- Execute `play_a_round(deck)`.
- Assert that:
  - `user_plays` is called exactly once with the human player and the deck.
  - `computer_plays` is called exactly once with the AI player and the deck.
- Push sub task to GitHub, [Go To GitHub Commit](#github-commit)

## Sub-task 5 – Test Game Lifecycle and Winner Flagging

To verify that `play()` invokes the full game sequence and flags the winner dictionary.

### Requirement

- Implement `test_play_orchestrates_lifecycle_and_flags_winner` in `test/test_twenty_one.py`.
- Mock the lifecycle helpers called by `play()`:
  - `initiate(no_of_cards, override)` -> returns a dummy deck.
  - `play_a_round(deck)`.
  - `reset_players()`.
  - `determine_winner()` -> returns a mutable mock player dictionary `{"name": "Dealer", WINNER: False}`.
  - `show_players()`.
- Assert that:
  - Each lifecycle step executes in the expected sequence.
  - The winner dictionary returned by `determine_winner()` has its `WINNER` field updated to `True`.
- Push sub task to GitHub, [Go To GitHub Commit](#github-commit)


# Run Tests

python -m pytest test/ -v

# GitHub Commit
* Open VS Code Terminal
* git add *
* git commit -m "sub task x complete"
* git push
