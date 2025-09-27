# Solution/Verification Tradeoffs in Reasoning Models

This project explores how to **predict the minimal reasoning token budget** needed for a verifier large language model (LLM) to check the correctness of math word problem solutions, reducing unnecessary computation while keeping accuracy high.

## Overview
Large Language Models generate hidden reasoning steps (“reasoning tokens”) to solve and verify problems, but longer reasoning costs more compute.  
We study how to efficiently allocate verification tokens without sacrificing correctness.

## Method
1. **Solution Generation:** Used **google/gemini-2.5-flash** to solve GSM8K math problems, producing final answers plus detailed reasoning.  
2. **Iterative Verification:** A second Gemini instance verified each solution with budgets from **4–512 tokens**.  
3. **Optimal Budget Dataset:** Recorded the smallest token budget that allowed correct verification for each problem.  
4. **Prediction Models:**  
   - Logistic Regression using `text-embedding-ada-002` embeddings.  
   - Fine-tuned `text-ada-001` to directly predict optimal budgets.

## Key Findings
- Over **95 %** of GSM8K problems can be correctly verified with only **64 tokens**.  
- Baseline model achieved **94.6 % accuracy**, mainly by predicting the dominant 64-token class.  
- Current verifier behavior shows **significant compute overuse**, often allocating more tokens than necessary.

## Future Work
- Apply to more complex reasoning datasets.  
- Use non-linear or transformer-based classifiers.  
- Frame as a regression task for finer-grained budget prediction.  
- Test cross-model generalization (e.g., GPT-4, Claude).

## Team
University of Bonn – CAISA NLP Lab  
**Team 9:** Umutcan Doğan  
Instructor: Prof. Dr. Lucie Flek  
Advisor: Dr. Florian Mai  

*Summer Semester 2025*
