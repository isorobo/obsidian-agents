# Project Audit

Run this at project close, not during design. It is a review instrument. It is
not a design checklist, and it never runs alongside the eight gates.

Answer every question. Where the answer is "no" or "unknown", that is the
finding. Record findings in the project note.

## 1. Objective

1. What was the stated learning objective?
2. Did Simon learn it? What is the evidence?
3. What did the project teach that nobody planned?
4. Could Simon rebuild this system without Claude? If not, which part fails?

## 2. Problem

5. Did the problem statement survive the build, or did it move?
6. Did the test defined in Gate 2 actually run?
7. Who used the result? If nobody, why was it built?

## 3. Agency

8. Did the agent decide anything that a fixed rule could have decided?
9. Which run-time unknown justified the agent? Did it hold?
10. Would the workflow option have worked? Answer honestly.
11. How often did the agent choose the same path a script would have chosen?

## 4. The loop

12. What was the maximum iteration count observed?
13. Did the stop condition ever fire? What happened next?
14. Did any run loop without progress?

## 5. Tools

15. Which tool was called most? Which was never called?
16. Which tool failed most? What happened when it did?
17. Did any tool return partial data without saying so?
18. Was every tool schema validated, or did any accept free text?

## 6. Context and memory

19. What was retained across runs? Was any of it read?
20. Did the context window ever overflow? What was lost?
21. Was retrieved content ever treated as instruction?

## 7. Prompt

22. How many times was the prompt edited?
23. Which instruction was added after a failure? That is a principle candidate.
24. Which instruction could be deleted with no effect? Delete it.

## 8. Evaluation

25. Did the three reference cases from the design stage exist before stage one?
26. How many cases exist now?
27. Which failure was caught by a test, and which by a user?
28. What is the current pass rate? If unmeasured, that is the finding.

## 9. Architecture

29. Which component from the recommended tier proved unnecessary?
30. Which component from the future tier turned out to be needed on day one?
31. What would the minimum architecture have cost in rework? Was the extra
    justified?
32. Is any component present because it was interesting rather than necessary?

## 10. Control

33. What did the agent do without asking? Was that the intended boundary?
34. Was anything irreversible? Who could stop it, and how fast?
35. Did the operator ever override the agent? Why?

## 11. Cost and operation

36. What does one run cost?
37. What is the slowest step, and does it matter?
38. What breaks first under ten times the load?
39. Who maintains this in six months?

## 12. Failure record

40. How many failures were logged?
41. Which class recurred? A repeat is a standing weakness.
42. Which failure produced a principle?
43. Which failure produced nothing? Process it now or discard it.

## 13. The vault

44. Which vault note answered a question during this project?
45. Which question the vault could not answer? Those are the gaps.
46. Which note is now wrong because of what this project showed?
47. What new concept note does this project justify?

## 14. Honest close

48. What would Simon do differently, stated as a rule rather than a regret?
49. What part of this system does Simon still not understand?
50. Should this system exist? If the answer is no, say so and archive it.

## Output

Propose one `project` note under `99_Meta/learning/`, carrying `topic/learning`
and one general topic. Propose ledger updates. Propose gap files for
`00_Inbox/`. Write nothing without approval.
