<h1>🧠 Tokenization in Large Language Models (LLMs)</h1>
<h3>A Rapid7 Security & AI Perspective</h3>

<p>
This document explains <b>tokenization</b>, its components, pipelines, and impact on
<b>LLMs used in security platforms</b>, with examples relevant to
<b>Rapid7 use cases</b> such as vulnerability management, SIEM, threat detection,
and security analytics.
</p>

<hr/>

<h2>📌 Table of Contents</h2>
<ol>
  <li>Introduction (Rapid7 Context)</li>
  <li>Basics of Tokens</li>
  <li>Tokenization Strategies</li>
  <li>Popular Tokenization Algorithms</li>
  <li>Tokenizer Architecture</li>
  <li>Tokenization Pipeline in LLMs</li>
  <li>Training vs Inference Tokenization</li>
  <li>Tokenizers in Popular LLMs</li>
  <li>Context Length & Token Limits</li>
  <li>Multilingual Tokenization</li>
  <li>Tokenization Challenges in Security</li>
  <li>Tokenization for Code & Logs</li>
  <li>Performance & Cost Considerations</li>
  <li>Custom Tokenizers for Security Domains</li>
  <li>Tools & Libraries</li>
  <li>Practical Security Examples</li>
  <li>Tokenization & Prompt Engineering</li>
  <li>Common Misconceptions</li>
  <li>Future Directions</li>
  <li>Summary</li>
</ol>

<hr/>

<h2>1. Introduction (Rapid7 Context)</h2>
<p>
Tokenization converts raw text into <b>tokens</b>, the atomic units LLMs understand.
At Rapid7, this directly affects how models process:
</p>
<ul>
  <li>Vulnerability descriptions (CVE, CVSS)</li>
  <li>Security logs (InsightIDR)</li>
  <li>Alerts and investigations</li>
  <li>Threat intelligence reports</li>
  <li>Natural language analyst queries</li>
</ul>

<h2>2. Basics of Tokens</h2>
<p>A token may represent:</p>
<ul>
  <li>A word (<code>vulnerability</code>)</li>
  <li>A subword (<code>auth</code>, <code>enticated</code>)</li>
  <li>A symbol (<code>{ }</code>, <code>:</code>)</li>
  <li>A byte (useful for logs and payloads)</li>
</ul>

<h3>Special Tokens</h3>
<ul>
  <li><code>&lt;bos&gt;</code> – Beginning of sequence</li>
  <li><code>&lt;eos&gt;</code> – End of sequence</li>
  <li><code>&lt;pad&gt;</code> – Padding</li>
  <li><code>&lt;unk&gt;</code> – Unknown tokens</li>
</ul>

<h2>3. Tokenization Strategies</h2>
<ul>
  <li><b>Word-based:</b> Simple but breaks on security identifiers</li>
  <li><b>Character-based:</b> No OOV issues, but inefficient</li>
  <li><b>Subword-based:</b> Best balance for security text</li>
  <li><b>Byte-level:</b> Ideal for logs and encoded input</li>
</ul>

<h2>4. Popular Tokenization Algorithms</h2>
<ul>
  <li><b>BPE (Byte Pair Encoding):</b> Used in GPT-style models</li>
  <li><b>WordPiece:</b> Used in BERT-like classifiers</li>
  <li><b>Unigram LM:</b> Probabilistic token selection</li>
  <li><b>SentencePiece:</b> Language-agnostic, whitespace independent</li>
</ul>

<h2>5. Tokenizer Architecture</h2>
<pre>
Raw Security Text / Logs
        ↓
Normalization
        ↓
Pre-tokenization
        ↓
Subword Encoding
        ↓
Token IDs
</pre>

<h2>6. Tokenization Pipeline in LLMs</h2>
<ol>
  <li>Raw input (alerts, logs, vulnerability text)</li>
  <li>Unicode normalization</li>
  <li>Token splitting</li>
  <li>Token-to-ID mapping</li>
  <li>Padding / truncation</li>
  <li>Attention mask generation</li>
</ol>

<h2>7. Training vs Inference Tokenization</h2>
<p>
<b>Training:</b> Tokenizer defines what the model can understand.<br/>
<b>Inference:</b> Token count impacts latency, cost, and throughput at Rapid7 scale.
</p>

<h2>8. Tokenizers in Popular LLMs</h2>
<table border="1" cellpadding="6">
  <tr>
    <th>Model Family</th>
    <th>Tokenizer</th>
  </tr>
  <tr>
    <td>GPT-style</td>
    <td>Byte-level BPE</td>
  </tr>
  <tr>
    <td>BERT-style</td>
    <td>WordPiece</td>
  </tr>
  <tr>
    <td>T5</td>
    <td>SentencePiece</td>
  </tr>
  <tr>
    <td>LLaMA / Mistral</td>
    <td>SentencePiece / BPE</td>
  </tr>
</table>

<h2>9. Context Length & Token Limits</h2>
<p>
Context limits matter when processing large alerts, multiple logs, or full investigations.
Tokens are not the same as words (≈ 0.75 English words per token on average).
</p>

<h2>10. Multilingual Tokenization</h2>
<ul>
  <li>Global customer data</li>
  <li>Localized OS logs</li>
  <li>Mixed-language investigations</li>
</ul>

<h2>11. Tokenization Challenges in Security</h2>
<ul>
  <li>Rare exploit names</li>
  <li>Zero-day terminology</li>
  <li>Obfuscated payloads</li>
  <li>High symbol density</li>
</ul>

<h2>12. Tokenization for Code & Logs</h2>
<pre>
GET /wp-admin/admin.php?user=admin HTTP/1.1
</pre>
<p>
Whitespace, symbols, and ordering are semantically meaningful in security logs.
</p>

<h2>13. Performance & Cost Considerations</h2>
<ul>
  <li>Token count affects API cost</li>
  <li>Long sequences increase latency</li>
  <li>Efficient tokenization improves SOC workflows</li>
</ul>

<h2>14. Custom Tokenizers for Security Domains</h2>
<p>
Custom tokenizers may benefit vulnerability databases, exploit frameworks,
and proprietary telemetry formats.
</p>

<h2>15. Tools & Libraries</h2>
<ul>
  <li>Hugging Face Tokenizers</li>
  <li>SentencePiece</li>
  <li>tiktoken</li>
  <li>spaCy</li>
</ul>

<h2>16. Practical Security Example</h2>
<pre>
CVE-2024-12345 allows remote code execution via deserialization.
</pre>

<h2>17. Tokenization & Prompt Engineering</h2>
<ul>
  <li>Prioritize high-signal fields</li>
  <li>Summarize logs before tokenization</li>
  <li>Avoid raw dumps where possible</li>
</ul>

<h2>18. Common Misconceptions</h2>
<ul>
  <li>Tokens are not words</li>
  <li>More tokens do not mean better understanding</li>
  <li>Tokenization does not infer meaning</li>
</ul>

<h2>19. Future Directions</h2>
<ul>
  <li>Token-free models</li>
  <li>Learned tokenizers for telemetry</li>
  <li>Multimodal tokenization</li>
</ul>

<h2>20. Summary</h2>
<p>
Tokenization is foundational to AI-powered security at Rapid7, directly impacting
accuracy, cost, and scalability of LLM-driven features.
</p>
