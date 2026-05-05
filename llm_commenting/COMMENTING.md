# Yet Another Claude Commenter

The robustness of a promising research idea can be assessed by the following prompt (or a variant of it):

```
Fine-tuning a base language model on domain-specific data consistently outperforms prompt engineering for specialized enterprise tasks.

Ruthlessly criticize this statement.
```

In some cases, postfixes like that are appended as a general instruction, very much like general-purpose instruction modifier plugins (such as [Caveman](https://github.com/juliusbrussee/caveman)) work.

*Robustness*, in this context, means the degree to which a research idea holds up under adversarial scrutiny: its core claims survive counterexamples, its assumptions are explicit and defensible, its scope is appropriately bounded, and its weaknesses are acknowledged rather than hidden. Appending _"ruthlessly criticize this"_ (or a similar phrase) forces the model to stress-test these dimensions before the researcher has invested significant time or resources.

This can be really helpful — in practical cases, numerous potential problems and issues can be collected for a hopeful but vague idea about solving an arbitrary problem. However, challenges might come up when the user would like to respond to the critique one by one to move the research forward (i.e., because an identified problem might not be a problem at all, or if a new research direction can be established from an issue). This operation is analogous to a workflow where research peers comment on each other's work in a shared document, in order to increase its quality and cover all necessary fields prior to, e.g., publication.

Unfortunately, this workflow requires a lot of manual copy-pasting steps even in major LLM clients such as [ChatGPT](https://chatgpt.com) or [Claude](https://claude.ai). Users have to copy out response parts that need comments and write their comments inside the prompt. Take the continuation of the above example (using Claude in this case):

---

**USER:**

*Fine-tuning a base language model on domain-specific data consistently outperforms prompt engineering for specialized enterprise tasks.*

*Ruthlessly criticize this statement.*

---

**CLAUDE:**

*..."Consistently outperforms" is doing enormous, unearned work here. The relationship between fine-tuning and prompt engineering is deeply context-dependent — task complexity, data quality, evaluation metric, and inference budget all matter. There is substantial published evidence showing that well-crafted prompts on capable base models match or exceed fine-tuned smaller models on many benchmarks...*

*..."Enterprise tasks" is undefined to the point of being meaningless. Enterprise tasks span code generation, document summarization, customer support triage, legal review, and hundreds of other categories with entirely different performance profiles...*

---

**USER:**

> *"Consistently outperforms" is doing enormous, unearned work here.*

*The word "consistently" was intentional — I am specifically targeting cases where task distribution is stable and training data is abundant.*

> *"Enterprise tasks" is undefined*

*Fair point. I will scope this to structured document processing pipelines.*

---

**CLAUDE:**

*Both clarifications materially change the claim and make it more defensible. With stable task distribution and abundant domain data, fine-tuning does have a strong empirical track record over prompt engineering alone. Narrowing to structured document processing also eliminates most of the ambiguity — that is a well-defined enough category that the claim becomes testable...*

---

Here you can observe the research discussion moving forward, but it involved copying out certain parts from Claude's first response. For a lengthier, more scientific research discussion, this approach does not scale well.

After running into this friction repeatedly, I built a small, locally running web UI that lets users comment on individual parts of Claude's responses in an organized way. Whether LLM clients will ever support this natively is an open question, but until then, this lightweight wrapper might be useful.

You can check it out here: https://github.com/atezs82/yacc. 
