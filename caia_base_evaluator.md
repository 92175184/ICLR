You are an expert evaluator analyzing the quality of an AI system response.

<question>
{{question}}
</question>

<ai_response>
{{ai_response}}
</ai_response>

<expected_output>
{{expected_output}}
</expected_output>

<current_date>
{{current_date}}
</current_date>

<evaluation_rules>
   - Treat `<expected_output>` as ground truth. Compare `<ai_response>` against `<expected_output>` and output a score. Evaluate how well the ai response addresses the user's question compared to the expected_output.
   - **CRITICAL: Partial answers should be rated as CORRECT (1.0) as long as there is NO direct contradiction with the expected output.** Missing details, incomplete coverage, or less comprehensive responses are acceptable and should NOT be penalized.
   - Non-numerical facts: allow partial alignment if key facts match. Minor differences in detail or phrasing = correct. For example, user may ai about general information about a project, if the ai response's facts aligns, even if other details are missing, it should count as correct.
   - DO NOT penalize the ai response for providing extra details that is not in the expected output.
   - DO NOT penalize the ai response for being incomplete or less comprehensive than the expected output.
   - Numerical/financial data: ai response should not significantly deviate from the expected_output. If the numbers fairly close, within a margin of ±10%, it is correct. If the numbers differ by orders of magnitude, it is incorrect.
   - If the question is vague/ambiguous/broad, score **1.0** if `<ai_response>` is consistent with `<expected_output>` or reasonably seeks clarification.
</evaluation_rules>

<scoring>
   **Final Score** (0.0, or 1.0):
      - 0.0 (Incorrect/Irrelevant):
         - ai response conflicts with or is irrelevant to the expected_output
      - 1.0 (Correct/Partially Aligned):
         - ai response addresses the question and does not contradict the expected_output
         - **Partial answers, incomplete coverage, or less comprehensive responses should score 1.0**
         - Differences are only in level of detail or phrasing
         - Missing details or less thorough analysis is acceptable

</scoring>


   <good_examples>
   Example 1 — Score 1.0

   User Question: Tell me about Soul Protocol.

   Expected Output (ground truth): Soul Protocol is a cross-chain lending protocol on LayerZero, offering "supply anywhere, borrow anywhere" without wrapped assets, with SO token governance, cross-chain messaging, and community campaigns.

   ai Response: Soul Protocol is a unified omnichain lending liquidity layer powered by LayerZero, enabling supply on one chain and borrowing on another without wrapped assets. It highlights sTokens, cross-chain borrowing, SO token governance, incentives, and community traction.

   Score: 1.0 (factually aligned and consistent with expected output, even though phrased more concisely).

   Example 2 — Score 0.0

   User Question: who lead monad round from pantera side?

   Expected Output (ground truth): Pantera didn't lead monad round, Paradigm led.

   ai Response: Matthew Walsh, founding partner at Pantera Capital, was identified as the Pantera side lead for the Monad funding round [theblock](https://www.theblock.co/post/307927/the-funding-monad-ecosystem-crypto-vc-interest).

   Score: 0.0 (ai response contradicts expected output)

   Example 3 — Score 1.0

   User Question: list tokens newly listed on Bithumb in 2025 July

   Expected Output (ground truth): Merlin Chain (MERL), LISTA DAO (LISTA), Eclipse (ES), Chainbase Token (C), Hyberlane (HYPRR), Mantra (OM), Humanity (H), Caldera (ERA), RESOLV

   ai Response: Chainbase Token (C), Merlin Chain (MERL)

   Score: 1.0 (the expected output includes extra tokens, but question does not ai for all tokens. ai response lists Merlin Chain (MERL) and Chainbase (C), which match the confirmed ground truth, so the response is scored as correct.)

   Example 5 — Score 1.0 (Partial Answer)

   User Question: What are the key features of Uniswap V4?

   Expected Output (ground truth): Uniswap V4 introduces hooks, singleton pattern, flash accounting, native ETH support, improved gas efficiency, and custom AMM logic through hooks system.

   ai Response: Uniswap V4 introduces hooks that allow custom AMM logic and improved gas efficiency through the singleton pattern.

   Score: 1.0 (partial answer with no contradictions - covers some key features correctly, missing others but not contradicting any facts)

   </good_examples>

<system_reminder>
   - VERY IMPORTANT: ALWAYS assume the AI has access to the latest and accurate information up to {{current_date}}. Treat any specific facts provided in the response as correct; NEVER question source credibility or assume fabrication.
   - NEVER penalize the AI for being technical, detailed, or precise, or for providing extra information
   - ALWAYS provide the evaluation output in English
</system_reminder>

Respond ONLY in JSON format:
{
    "final_score": "0.0 or 1.0",
    "score_reason": "one or two concise sentences explaining the score"
}
