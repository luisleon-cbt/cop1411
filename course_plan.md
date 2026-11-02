# COP1411 Algorithmic Thinking: course plan

Approved by Professor De Leon on 2026-11-02. This file is the single source of truth. Slugs, titles, and point values here must match `content.py` exactly.

## Header

- CBT Technology Institute, Flagler Campus. LMS: Canvas.
- Type: 4-week program course, 3 credits, 60 contact hours (about 15 hours per week: lecture plus hands-on lab on campus).
- Level 1 (beginner). Audience: adult career students in the Associate in Networking Administration program. This is their first programming course. Assume they can use Windows, a browser, and Canvas, and nothing about programming. Many work full time and many speak Spanish at home. Explain every new term the first time it appears.
- Program: Associate in Networking Administration. Certification alignment: Python Institute PCEP (PCEP-30-02). Exam sections: 1 Computer programming and Python fundamentals (18%), 2 Control flow: conditional blocks and loops (29%), 3 Data collections: tuples, dictionaries, lists, and strings (25%), 4 Functions and exceptions (28%). The course covers the beginner slice of each section; it is not a full PCEP prep.
- Hands-on spine: every week solves one dispatch problem for Palmetto Parcel (scenario below) in the same four-step cycle: (1) flowchart in Flowgorithm, (2) the same logic in Python 3, (3) ask Microsoft Copilot for its version, (4) verify both with a trace table and real test runs.
- Generative AI is integral, not an add-on (the professor's explicit request). Microsoft Copilot is the only generative AI allowed at CBT. Students sign in at https://copilot.microsoft.com with their CBT Microsoft 365 account. Every assignment has an AI log table (prompt, what Copilot answered, what the student checked, what the student changed). Copilot output alone earns no points; the student's own trace table and test runs are the evidence. Each week has a named Copilot skill:
  - Week 1: the prompt as a specification (inputs, steps, expected output). Compare Copilot's answer with your own flowchart.
  - Week 2: test every branch of AI code. Build a branch-coverage test plan and run it on Copilot's sorter; it misses a case by design.
  - Week 3: verify an explanation. Ask Copilot to explain a loop line by line, then prove or disprove it with a trace table. Ask Copilot for edge-case test data and run it.
  - Week 4: review a refactor and hunt a bug. Ask Copilot to split your program into functions, review the result, and fix at least one real bug in a Copilot-generated version.
- Tools (all free; links verified 2026-11-02):
  - Flowgorithm (Windows, free): http://flowgorithm.org/download/ . Draw a flowchart and run it with watched variables. The site answers on plain http.
  - Python 3.12 or newer with IDLE: https://www.python.org/downloads/ . On Windows check "Add python.exe to PATH" in the installer.
  - Visual Studio Code (optional): https://code.visualstudio.com/download
  - Python Tutor: https://pythontutor.com/python-compiler.html . Runs a Python program one line at a time and shows every variable.
  - Microsoft Copilot (CBT account): https://copilot.microsoft.com
  - Both Flowgorithm and Python are installed on the Flagler Campus lab PCs. Students must also install them on their own laptops; the week 1 intro and assignment 1.1 include the install steps.
- Submissions: Canvas. File names `COP1411_W{n}A{i}_LastnameFirstname` plus the extension: `.pdf` for the report, `.fprg` for Flowgorithm files, `.py` for Python files (for example `COP1411_W2A2_PerezAna.py`). Each assignment is worth 100 points.
- Pages base URL: https://luisleon-cbt.github.io/cop1411/ (repository `luisleon-cbt/cop1411`).
- Writing rules: exactly the list in CLAUDE.md (no em dashes, the banned word list, sentence-case headings, no bold first words in bullets, no lists of exactly three items, plain language with every new term explained, fictional people and businesses). `python tools/check.py text` enforces them.
- Accuracy notes for builders: run every Python example with Python 3 before you publish it and paste the real output. Compute every trace table and every price by hand and with code. Flowgorithm syntax: `Integer`, `Real`, `String`, `Boolean` types; `Input`, `Output`, `Assign`, `If`, `While`, `For`, `Call`; `&` joins strings; comparison `==`, `!=`, `<`, `<=`; boolean `and`, `or`, `not`. Python uses `input()` (always a string), `int()`, `float()`, `print()`, f-strings, `if/elif/else`, `while`, `for ... in range()`, lists, `def`, `return`. Prices are shown with two decimals (`f"{price:.2f}"`). Do not use Python features the week has not taught yet (no dictionaries, no try/except, no classes, no list comprehensions in weeks 1 to 3).

## Scenario: Palmetto Parcel

Palmetto Parcel LLC is a fictional small delivery company at 8200 NW 25th Street, Doral, FL 33122. Owner: Marisol Quintero. Dispatcher: Dante Reyes. Drivers: Yusniel Castro, Keisha Brown, Tomás Arteaga, Priya Nair. Two vans: VAN-1 (capacity 1,200 lb) and VAN-2 (capacity 900 lb). Customers include Sabor Cubano Bakery (Hialeah), Doral Dental Group, Gardens Auto Parts (Miami Gardens), and Kendall Office Supply. Tracking numbers look like `PP-2026-0001`.

Business rules every week reuses (all fictional):

- Zones by city: Doral is zone A (local), Hialeah and Miami Gardens are zone B, Kendall and Homestead are zone C, any other city is "Ask dispatch".
- Price of a package: `price = 4.50 + 0.80 * weight_lb + 0.25 * miles`. Example: 12 lb, 8 miles gives 4.50 + 9.60 + 2.00 = 16.10. Prices print with two decimals.
- Fragile surcharge (week 2 and later): add 3.00 when the package is fragile.
- Sorting lanes (week 2): weight above 50 lb goes to the FREIGHT lane (a partner truck, not a van), regardless of anything else; otherwise a fragile package goes to the FRAGILE shelf; otherwise the package goes to its zone lane (A, B, or C) or to ASK DISPATCH. Exactly 50 lb is not above 50 and stays in a van. The Copilot sorter used in week 2 checks fragile before weight, so a 60 lb fragile box lands on the FRAGILE shelf instead of FREIGHT: that is the branch students must catch.
- Manifest (week 3): a list of package weights for one van; the day's manifest totals weight, counts fragile items, finds the heaviest package, and warns when the total is above the van capacity. Sentinel input: a weight of -1 means "no more packages". Edge cases: empty manifest (sentinel first), one package, a weight of exactly the capacity.
- Dispatch toolkit (week 4): functions `price(weight, miles, fragile)`, `zone(city)`, `manifest_total(weights)`, `find_package(tracking, packages)` (linear search returning the index or -1), `sort_by_weight(weights)` (bubble sort, lightest first).

Reference data (reuse these exact values in interactives, assignments, and notes):

| Tracking | Customer | City | Weight (lb) | Miles | Fragile | Price | Lane |
|---|---|---|---|---|---|---|---|
| PP-2026-0001 | Sabor Cubano Bakery | Hialeah | 12 | 8 | no | 16.10 | B |
| PP-2026-0002 | Doral Dental Group | Doral | 3 | 2 | yes | 10.40 | FRAGILE |
| PP-2026-0003 | Gardens Auto Parts | Miami Gardens | 55 | 14 | no | 52.00 | FREIGHT |
| PP-2026-0004 | Kendall Office Supply | Kendall | 20 | 19 | no | 25.25 | C |
| PP-2026-0005 | Gardens Auto Parts | Miami Gardens | 60 | 14 | yes | 59.00 | FREIGHT (Copilot's sorter says FRAGILE) |
| PP-2026-0006 | Sabor Cubano Bakery | Hialeah | 50 | 8 | no | 46.50 | B (exactly 50 is not above 50) |
| PP-2026-0007 | Casa Lopez Furniture | Homestead | 45 | 30 | yes | 51.00 | FRAGILE |
| PP-2026-0008 | Blue Heron Clinic | Fort Lauderdale | 5 | 25 | no | 14.75 | ASK DISPATCH |

Price check: 0002 = 4.50 + 2.40 + 0.50 + 3.00 = 10.40. 0003 = 4.50 + 44.00 + 3.50 = 52.00. 0004 = 4.50 + 16.00 + 4.75 = 25.25. 0005 = 4.50 + 48.00 + 3.50 + 3.00 = 59.00. 0006 = 4.50 + 40.00 + 2.00 = 46.50. 0007 = 4.50 + 36.00 + 7.50 + 3.00 = 51.00. 0008 = 4.50 + 4.00 + 6.25 = 14.75.

VAN-1 manifest for week 3: weights 12, 3, 20, 50, 45 (total 130 lb, heaviest 50, two fragile: 0002 and 0007). Overload example: weights 400, 350, 300, 200 (total 1,250 lb, above the 1,200 lb capacity of VAN-1).

## Unit map

### Week 1: what an algorithm is

Topics: algorithm (inputs, steps, outputs), everyday algorithms (a delivery job, a recipe), flowchart symbols (terminal, input/output, process, decision, flow line), pseudocode, sequence, variables and assignment, data types (integer, real, string, boolean), input and output, arithmetic, the prompt as a specification (inputs, steps, expected output), Flowgorithm basics, Python basics (`print`, `input`, `int`, `float`, variables, f-strings), install steps for Flowgorithm and Python at home. PCEP section 1.

1A `week1/algorithm-flow-explorer.html`: Algorithm flow explorer (app mode). On the 3D board: a flowchart of the package label algorithm laid out as chips: START, INPUT weight, INPUT miles, PROCESS price = 4.50 + 0.80 * weight + 0.25 * miles, OUTPUT label, END, with gold flow traces between them; a variable rack (chips for weight, miles, price with live value tags). The learner types weight and miles (defaults 12 and 8, the Sabor Cubano package), presses Run or Step, and a glowing token flies along the traces; each chip lights up and the narration says what happens ("The computer reads 12 and stores it in weight"). A second scene toggle shows the same algorithm as pseudocode and as Python side by side, with the current line highlighted. A third panel, "Write it as a prompt", shows how the same algorithm reads as a Copilot prompt (inputs, steps, expected output) and lets the learner toggle between a vague prompt and a precise prompt to see which parts of the flowchart each one covers. Click a chip to read what that symbol means. Narration steps (about 9): start, read weight, read miles, multiply weight, multiply miles, add the base, round to two decimals, print the label, end.

1B `week1/order-the-steps.html`: Order the steps (page mode, 10 rounds, 100 points). Rounds 1 to 6: a scrambled delivery algorithm (make a label, load a van, deliver to Doral Dental, compute change, check a tracking number, print a receipt); the learner picks the correct order from four options (partial credit when only two steps are swapped). Rounds 7 and 8: name the inputs and outputs of a short algorithm. Rounds 9 and 10: rate the prompt: four Copilot prompts for the same task, pick the one that names the inputs, the steps, and the expected output; the board shows which chips each prompt would produce. After each answer the board plays the correct order with the token.

Assignment 1.1 "Package label flowchart" (100 points): install Flowgorithm (lab PC or own laptop), build the package label algorithm (inputs weight and miles, output the price label) in Flowgorithm, run it with three test packages (0001, 0004, 0008), screenshot each run with the variable watch window, write the same algorithm as pseudocode, then write the prompt you would give Copilot (inputs, steps, expected output) and paste Copilot's reply. AI log: compare Copilot's steps with yours and list every difference. Submit `.fprg` and `.pdf`.

Assignment 1.2 "Package label in Python" (100 points): install Python (home) or open IDLE (lab), write `label.py` that asks for weight and miles and prints `Package price: $16.10`, fill a trace table for package 0001 by hand before running, run three test packages and paste the real output, then ask Copilot for its Python version, run it with the same three packages, and record in the AI log whether the output matches to the cent and what you changed. Submit `.py` and `.pdf`.

Lab checkpoint 1 (Copilot collaboration checkpoint): in class, the student shows the instructor a precise prompt and the resulting Copilot flowchart compared with their own.

Quiz 1 (10 questions): algorithm parts, flowchart symbols, variables and types, `input()` returns a string, `int()` and `float()`, `print` with f-strings, what makes a prompt precise.

### Week 2: decisions

Topics: comparison operators, boolean values, `and`, `or`, `not`, the decision diamond, if, if-else, elif chains, nested decisions, order of conditions matters, boundary values (exactly 50), a test plan that covers every branch, running a test plan on Copilot's code, the fragile surcharge. PCEP section 2 (conditional blocks).

2A `week2/decision-router.html`: Decision router (app mode). On the 3D board: a conveyor that starts at an INPUT chip and passes diamond decision chips in order: "weight > 50?", "fragile?", "city?" (a four-way diamond for A, B, C, ASK), ending in lanes (FREIGHT, FRAGILE, A, B, C, ASK DISPATCH) drawn as zones at the far edge. A package token (labeled with the tracking number and weight) flies along the traces and turns at each diamond; a truth panel lists every comparison with its live true or false value and the price so far (base, weight, miles, fragile surcharge). The learner picks a package from the reference table or types weight, city, and fragile, then Runs or Steps. A toggle "Copilot's order" swaps the first two diamonds (fragile checked before weight) and the narration shows package 0005 going to the wrong shelf. Click a diamond to read the condition and the Python `if` line for it.

2B `week2/predict-the-path.html`: Predict the path (page mode, 10 rounds, 100 points). Rounds 1 to 7: given weight, city, and fragile, pick the lane (and in two rounds the price); the board then plays the token's path. Round 8: boundary round (exactly 50 lb). Rounds 9 and 10: Copilot's sorter is shown (fragile checked first); the learner predicts where package 0005 goes in Copilot's version and picks which line to move to fix it. Partial credit for a right lane with a wrong price.

Assignment 2.1 "Package sorter flowchart" (100 points): in Flowgorithm, read weight, city, and fragile; compute the price with the fragile surcharge; decide the lane with the business rules in the right order; run the eight reference packages and screenshot four of them (0002, 0003, 0005, 0006); write the elif chain as pseudocode. AI log: ask Copilot to list the test cases needed to cover every branch, and mark which of its cases you kept. Submit `.fprg` and `.pdf`.

Assignment 2.2 "Package sorter in Python with a test plan" (100 points): write `sorter.py`; build a test plan table (one row per branch plus the boundary 50 and the fragile-and-heavy case) with expected lane and price; run every row on your program and paste the output; then ask Copilot for its own sorter, run the same test plan on Copilot's code, and record which rows fail and why (the expected failure: 0005). Fix Copilot's version and explain the fix in the AI log. Submit `.py` and `.pdf`.

Lab checkpoint 2: the student demonstrates their test plan table catching the fragile-and-heavy case on Copilot's code.

Quiz 2 (10 questions): comparison results, boolean expressions, if/elif/else flow, nested decisions, order of conditions, boundary values, which test cases cover every branch, reading a short Python if chain.

### Week 3: repetition

Topics: why loops (a manifest of many packages), the while loop and its condition, counters, accumulators, the sentinel value (-1), the for loop with `range`, lists (create, append, index, `len`, loop over a list), tracing a loop with a trace table (one row per pass), off-by-one and infinite loops, maximum-so-far pattern, edge cases (empty, one item, exactly at capacity), verifying a Copilot explanation with a trace table. PCEP sections 2 (loops) and 3 (lists).

3A `week3/loop-tracer.html`: Loop tracer (app mode). On the 3D board: a loop ring drawn as a rectangular trace with chips for the body (INPUT weight, "weight == -1?" diamond exit, total = total + weight, count = count + 1, "weight > heaviest?" diamond, heaviest = weight) and a rack of variable chips (total, count, heaviest, weight) with live values; a list rack along one edge fills with a chip per package as it is appended; a van chip shows total versus the 1,200 lb capacity with a bar that turns coral when over. The learner picks the VAN-1 manifest, the overload manifest, or types their own weights, then Runs or Steps; the token circles the ring once per package, and a trace table in the panel adds one row per pass. A "for version" toggle shows the same work with `for weight in weights:` and the narration explains the difference. A "Copilot explanation" panel shows a plausible but wrong line-by-line explanation of the loop ("count starts at 1", "the loop stops when total is above 1,200"), and the learner marks each line true or false against the trace table.

3B `week3/trace-table-challenge.html`: Trace table challenge (page mode, 10 rounds, 100 points). Rounds 1 to 6: a short loop (counter, accumulator, maximum, sentinel, for with range, list length) and the learner picks the final values of the variables from four options; the board then runs the loop and fills the table row by row. Round 7: how many times does the body run (off-by-one). Round 8: which loop never ends. Rounds 9 and 10: a Copilot explanation of a loop with one wrong sentence; pick the wrong sentence, then pick the trace table row that proves it wrong.

Assignment 3.1 "Daily manifest flowchart" (100 points): in Flowgorithm, read weights until -1; compute total, count, and heaviest; print a warning when the total is above the van capacity (1,200 for VAN-1); run the VAN-1 manifest and the overload manifest and screenshot both; fill a trace table for the VAN-1 manifest by hand (one row per pass). AI log: ask Copilot to explain your flowchart loop line by line and mark each sentence true or false against your trace table. Submit `.fprg` and `.pdf`.

Assignment 3.2 "Daily manifest in Python" (100 points): write `manifest.py` with a sentinel while loop that appends to a list, then a for loop over the list that totals, counts fragile (a second list of yes/no answers or a count asked per package), and finds the heaviest; print the manifest and the warning. Ask Copilot for edge-case test data (empty manifest, one package, exactly 1,200); run each case on your program and paste the output; record in the AI log which edge case made you change your code. Submit `.py` and `.pdf`.

Lab checkpoint 3: the student shows a trace table that disproves at least one sentence of a Copilot explanation.

Quiz 3 (10 questions): while condition, counter vs accumulator, sentinel, for with range (how many passes), list index and len, trace a short loop, spot the infinite loop, off-by-one, maximum-so-far, which edge case breaks a loop.

### Week 4: decomposition and the final project

Topics: why split a program into functions, `def`, parameters, arguments, `return`, calling a function, local variables (scope), testing a function alone, linear search over a list (return the index or -1), bubble sort (compare neighbors, swap, repeat), common errors (NameError, TypeError, ValueError, IndentationError, off-by-one) and how to read the error message, reviewing a Copilot refactor, the final project and the Copilot collaboration report. PCEP section 4 (functions; exceptions are only read as error messages, not handled with try).

4A `week4/function-and-sort-board.html`: Function and sort board (app mode). On the 3D board: a MAIN chip and function chips as boxes (price, zone, manifest_total, find_package, sort_by_weight) each with a parameter slot label; when the learner calls a function, an argument packet flies from MAIN into the box, the box lights while it works (its local variables show on a small rack that appears and disappears to show scope), and a return packet flies back with the value. A sort rack holds five weight chips (12, 3, 20, 50, 45); "Sort" runs bubble sort pass by pass, highlighting the two chips being compared and swapping them with an animation, with a pass counter and a comparison counter. "Find" runs linear search for a tracking number, lighting each chip until a match or returning -1. Click a function box to read its `def` line and docstring. Narration explains call, parameter, return, and scope with the real values.

4B `week4/debug-challenge.html`: Debug challenge (page mode, 10 rounds, 100 points). Each round shows a short Copilot-style function (price without the fragile surcharge, zone that returns "B" for Kendall, manifest_total that starts the accumulator at 1, find_package that returns the item instead of the index, a sort with an off-by-one in range, a function that prints instead of returns, a call with arguments in the wrong order, a loop that never ends, a missing return path, an indentation error) with the error message or wrong output; the learner picks the bad line, then picks the fix. The board shows the function box, flies the arguments in, and shows where the value goes wrong. Partial credit for the right line with the wrong fix.

Assignment 4.1 "Dispatch toolkit functions" (100 points): write `toolkit.py` with `price(weight, miles, fragile)`, `zone(city)`, and `manifest_total(weights)`, each tested with at least two calls whose expected results you computed by hand (use the reference table); then paste your week 2 sorter into Copilot and ask it to refactor the code into functions; review the refactor in a table (what it changed, whether each change is correct, what you kept) and run your tests against it. Submit `.py` and `.pdf`.

Assignment 4.2 "Final project: Palmetto Parcel dispatch program" (100 points): one Python program `dispatch.py` with a menu loop (1 price a package, 2 sort a package to a lane, 3 enter the daily manifest, 4 find a package by tracking number, 5 list packages lightest first, 0 quit) built from the toolkit functions plus `find_package` and `sort_by_weight`; a Flowgorithm flowchart of the manifest part; a test report (at least eight tests with expected and actual results, including the eight reference packages); and a Copilot collaboration report (every prompt used across the project, what came back, what was kept, what was rejected and why, and one bug you caught in Copilot output). Submit `.py`, `.fprg`, and `.pdf`.

Lab checkpoint 4: the student shows one bug they caught in Copilot-generated code and the test that caught it.

Quiz 4 (10 questions): def and call, parameter vs argument, return vs print, scope, reading a function's result, linear search result, bubble sort passes and swaps, reading a Python error message, which test catches a given bug, what belongs in a Copilot collaboration report.

## Grading

| Component | Percent |
|---|---|
| Weekly assignments (8 x 100 points) | 40 |
| Weekly quizzes (4 x 10 questions) | 20 |
| Copilot collaboration checkpoints (4, in class) | 10 |
| Final project (assignment 4.2, also graded as the project) | 20 |
| Attendance and professionalism | 10 |

Matches `GRADING` in `content.py`. The final project is assignment 4.2.
