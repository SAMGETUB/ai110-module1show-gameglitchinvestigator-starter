# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
Answer :
When I first ran the game, everything looked fine visually. However, when I started testing the features, I noticed several bugs. The first bug I found was that the hints were not working correctly. 
I expected the game to tell me to go higher when my guess was too low, but instead it was telling me to go higher even though when I inputted the number it was still glitching. The second bug was that the secret number kept changing. I expected it to stay the same until I won, but instead the secret number was changing after each attempt. The third bug was the restart feature. I expected a button to restart the game, but instead the game seemed to be stuck and I couldn't get a new instance of the game when clicking start a new game.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

For this project I used two AI tools: GitHub Copilot in VS Code and Claude as my pair programmer.

One example of a correct AI suggestion was when I asked Copilot to fix the inverted hints in check_guess, remove the block that converted the secret number to a string on even attempts, and move the logic functions into logic_utils.py. Copilot did all of this correctly and even updated the tests automatically. I verified it was correct by running pytest and seeing all 3 tests pass.

One example of an incorrect suggestion was when pytest could not find logic_utils. Claude suggested running touch tests/init.py to fix the import error, but that did not fully solve the problem. Copilot gave a better fix because it had more context about the project structure. This taught me that giving AI tools more context about your project leads to better suggestions.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

I decided a bug was really fixed by testing it two ways. First I manually tested the game in the browser, checking that hints were correct and that the secret number stayed the same on even attempts. Second I ran pytest in the terminal which collected 3 tests from test_game_logic.py and all 3 passed, confirming my fixes worked in code.

The tests Copilot generated tested three scenarios: a winning guess where 50 equals 50, a guess too high where 60 against secret 50 returns Too High with Go LOWER, and a guess too low where 40 against secret 50 returns Too Low with Go HIGHER.

I did not ask Copilot to design the tests — it created them automatically when it refactored the code. This showed me that good tests check specific inputs and expected outputs, and that AI can generate useful tests even without being asked.

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Streamlit is a Python library that turns Python code into a web app. Every time you interact with it, like clicking a button or submitting a guess, it reruns the entire app.py from top to bottom. This means normal variables reset on every click, which is why the secret number kept changing in our buggy game.
Session state is like a memory box that preserves variables like guesses after each rerun. Without it, the secret number would change after each failed attempt, making it impossible to win. With session state, the secret number gets created once and is preserved so that when we fail a guess and try again, we don't lose it

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse in future projects is testing specific behaviors after identifying and fixing a bug. Instead of assuming a fix works, I learned to check the exact edge cases I identified, verify through both manual testing and pytest, and if something is still unclear, ask another AI to look over the code and spot anything I missed.
Next time I work with AI on a coding task I would write more precise prompts so the AI doesn't go beyond what I specifically asked for. Copilot tends to do too much, so being more specific upfront saves time reviewing unnecessary changes.
This project changed the way I think about AI generated code. It made me realize that AI agents are really useful and time efficient — instead of going to Stack Overflow or searching for other developers with the same issue, we now have a personal assistant built into VS Code. But AI can make mistakes, so we still need to be in the driver's seat, verify everything it does, and make sure its output actually works."