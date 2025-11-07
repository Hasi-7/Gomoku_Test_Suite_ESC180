# Gomoku Test Suite

A comprehensive testing suite for Gomoku (Five in a Row) implementations. This test suite contains 76 tests covering basic functionality, edge cases, and potential bugs.

## 📋 What's Included

This test suite contains three test files:

1. **`test_gomoku.py`** (8 tests) - Basic pytest-style tests
2. **`test_gomoku_runner.py`** (8 tests) - Lightweight runner (no pytest required)
3. **`test_gomoku_edge_cases.py`** (60 tests) - Comprehensive edge case testing

## 🎯 What Gets Tested

### Core Functionality
- ✅ Board creation and empty board detection
- ✅ Sequence placement on board
- ✅ Boundary detection (OPEN, SEMIOPEN, CLOSED)
- ✅ Row/column/diagonal sequence detection
- ✅ Win condition detection (5 in a row)
- ✅ Draw detection (full board, no winner)
- ✅ Scoring algorithm
- ✅ AI move selection (`search_max`)

### Edge Cases Covered
- 🔲 **Board Boundaries**: Sequences at corners, edges, and boundaries
- 🔄 **Sequence Detection**: Single stones, gaps, overlapping sequences, parallel sequences
- 🏆 **Win Conditions**: Horizontal, vertical, diagonal (both slopes), 5+ in a row
- 🤖 **AI Logic**: Winning moves, blocking opponent, empty board, full board
- 🔍 **Special Patterns**: Blocked sequences, forks, double threats, mid-game positions

## 🚀 Quick Start

### Prerequisites

Your Gomoku implementation must have these functions available:
```python
make_empty_board(size)
put_seq_on_board(board, y, x, d_y, d_x, length, col)
is_empty(board)
is_bounded(board, y_end, x_end, length, d_y, d_x)
detect_row(board, col, y_start, x_start, length, d_y, d_x)
detect_rows(board, col, length)
score(board)
search_max(board)
is_win(board)
print_board(board)  # Optional, only needed for one test
```

### Installation

1. Clone or download this repository
2. Place your `gomoku.py` file in the same directory as the test files
3. Choose your testing method below

## 🧪 Running the Tests

### Option A: Using pytest (Recommended)

**Install pytest:**
```bash
pip install pytest
```

**Run all tests:**
```bash
pytest -v
```

**Run specific test file:**
```bash
pytest test_gomoku.py -v
pytest test_gomoku_edge_cases.py -v
```

**Run and see coverage:**
```bash
pytest --tb=short
```

### Option B: Without pytest (Standalone Runners)

**Run the basic test runner:**
```bash
python test_gomoku_runner.py
```

**Run the comprehensive edge case suite:**
```bash
python test_gomoku_edge_cases.py
```

Both standalone runners will:
- Print PASS/FAIL for each test
- Show which tests failed with error messages
- Exit with code 0 (success) or 1 (failure)

## 📊 Expected Results

If your implementation is correct, you should see:
```
All tests passed
```

If there are bugs, you'll see output like:
```
FAIL: test_more_than_five_in_a_row -> 7 stones in a row should be detected as a win
FAIL: test_search_max_blocks_opponent_win -> Should block at (3,0) or (3,5), got (None,None)

5 test(s) failed
```

## 🐛 Common Bugs Detected

This test suite is designed to catch these common Gomoku implementation bugs:

### 1. Long Sequences Not Detected as Wins
**Symptom:** 6, 7, or 8 stones in a row don't register as a win
**Test:** `test_more_than_five_in_a_row`, `test_detect_row_entire_row_filled`

### 2. search_max Returns None
**Symptom:** AI fails to return a move even when legal moves exist
**Test:** `test_search_max_one_empty_cell`, `test_search_max_blocks_opponent_win`
**Common cause:** `best_score` initialized to 0, moves with negative scores ignored

### 3. AI Doesn't Block Opponent Wins
**Symptom:** AI doesn't recognize when opponent has 4 in a row
**Test:** `test_search_max_blocks_opponent_win`

### 4. Boundary Sequences Not Properly Handled
**Symptom:** Sequences touching board edges aren't detected correctly
**Test:** Various boundary tests in `test_gomoku_edge_cases.py`

### 5. Exact Length Matching Issue
**Symptom:** `detect_rows()` only finds sequences of exactly the specified length
**Test:** `test_board_exactly_5x5`

## 🎓 For Students & Learning

This test suite is designed for:
- ✏️ **Course Projects**: Validate your Gomoku assignment
- 🐞 **Debugging**: Identify specific issues in your implementation
- 📚 **Learning**: Understand edge cases and proper testing practices
- 🤝 **Collaboration**: Share with classmates to ensure everyone's code works

## 📝 Test File Details

### test_gomoku.py
Basic functionality tests using pytest. Good for quick validation.
- Board basics
- Sequence detection
- Scoring
- Win conditions

### test_gomoku_runner.py
Same as above but doesn't require pytest installation. Perfect for sharing with friends who might not have pytest.

### test_gomoku_edge_cases.py
Comprehensive edge case testing (60 tests):
- Board boundaries (9 tests)
- Sequence detection edge cases (11 tests)
- Win detection edge cases (9 tests)
- Scoring edge cases (9 tests)
- AI (search_max) edge cases (6 tests)
- Row detection specifics (4 tests)
- Boundary detection specifics (4 tests)
- Helper function tests (3 tests)
- Complex game scenarios (5 tests)

## 🔧 Customization

### Testing Your Own Board Size
By default, all tests use 8x8 boards. To test different sizes, modify the `make_empty_board()` calls in the test files.

### Adding Your Own Tests
Follow this pattern:
```python
def test_your_new_test():
    """Description of what you're testing"""
    b = make_empty_board(8)
    # Set up your test scenario
    put_seq_on_board(b, 0, 0, 0, 1, 5, 'b')
    # Assert expected behavior
    assert_equal(is_win(b), 'Black won')
```

Then add your test function to the `tests` list in `main()`.

## 📦 File Structure
```
gomoku-test-suite/
├── README.md                      # This file
├── test_gomoku.py                 # Basic pytest tests
├── test_gomoku_runner.py          # Standalone basic tests
└── test_gomoku_edge_cases.py      # Comprehensive edge cases
```

**Your gomoku.py should be in the same directory as the test files.**

## 🤝 Contributing

Found a bug the tests don't catch? Have an edge case to add? 
- Add your test case following the existing patterns
- Make sure it tests for **correct behavior**, not buggy behavior
- Include a descriptive docstring
- Test on an 8x8 board for consistency

## 📄 License

Free to use for educational purposes. Share with your classmates, study groups, and friends!

## ⚠️ Important Notes

- All tests assume an **8x8 board** is the default
- Tests check for correct Gomoku rules (exactly 5 in a row wins)
- The test suite validates **functionality**, not code style
- Tests are designed to **find bugs**, not to pass on buggy code

## 💡 Tips for Using These Tests

1. **Run tests frequently** as you develop
2. **Fix one test at a time** - don't try to fix everything at once
3. **Read the test descriptions** to understand what's being checked
4. **Use test failures as debugging clues** - they tell you exactly what's wrong
5. **Start with basic tests** before moving to edge cases

## 🎉 Credits

Created for ESC180 Gomoku Project testing.
Developed to help students identify and fix common implementation bugs.

---

**Happy Testing! 🎮**

If these tests helped you find bugs in your code, consider sharing this test suite with your friends!
