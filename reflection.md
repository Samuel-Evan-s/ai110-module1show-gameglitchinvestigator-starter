# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

The first time I ran the game, the hints text was wrong (e.g., "Go HIGHER" when my guess was too high), and the game stopped as if I had lost before I used all attempts. The new game button also sometimes reset the secret to a fixed 1-100 range instead of honoring the selected difficulty range.

Bugs I observed:
- Hints were backwards (wrong direction words).
- The game over condition and attempt accounting were off (attempt count started at 1 and could end too soon).
- New game did not always fully reset state to a fresh playing round.

---

## 2. How did you use AI as a teammate?

I used Copilot (the VS Code AI assistant) as a teammate in this project. I asked it to refactor core logic into `logic_utils.py` and to spot where the bug in `check_guess` and attempt handling were located.

Correct AI suggestion: It correctly suggested moving the helper functions (`check_guess`, `parse_guess`, and `update_score`) into `logic_utils.py` and updating `app.py` imports. I verified by running tests and confirming the game still worked.

Incorrect/misleading AI suggestion: The initial generated `check_guess` in the starter app included a weird string casting branch and reversed hint messages. I verified by reading the logic and running the unit tests, then I corrected it explicitly in `logic_utils.py`.

---

## 3. Debugging and testing your fixes

I decided a bug was fixed when both automated tests and manual game behavior matched expected outcomes. For the direction bug, I updated `check_guess` and verified that a guess of 60 vs secret 50 returned "Too High" with "LOWER" in the message.

One test I ran: `python -m pytest -q` after adding a regression test `test_guess_wrong_direction_bug_fixed` that asserts `check_guess(70, 50)` returns "Too High" and includes "LOWER". It passed, which confirmed the fix.

AI helped by suggesting test structure and by making me focus on small regression tests for specific bugs.

---

## 4. What did you learn about Streamlit and state?

Streamlit reruns the script on every user interaction, so all code runs again from top to bottom. Session state is how you keep game variables (`secret`, `attempts`, `status`) persistent across reruns; if you don't store them in `st.session_state`, they reset each click.

---

## 5. Looking ahead: your developer habits

One habit I want to reuse is writing minimal regression unit tests for each bug and running `pytest` frequently. Another is moving logic out of UI code for easier testing.

Next time with AI, I will validate suggested changes immediately with small tests before accepting larger refactors.

This project reinforced that AI-generated code can be a strong starting point, but you must verify and fix logic carefully with tests.

