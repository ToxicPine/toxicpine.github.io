---
title: Introducing EasyLLMBench
date: 2025-04-20 07:00:00 +0000
categories: [Technology, Artificial Intelligence]
tags: [benchmarks, llm, ai]
---

**TL;DR:** I made a [tool for benchmarking LLMs that doesn't suck.](https://github.com/ToxicPine/easybench)

We're often told about vague, subjective leaps in quality – remember the hype around GPT-4.5's supposed "subtle intelligence"? Yeah, clever prompting and wishful thinking can make these claims seem real. 

Thankfully, benchmarks are an excellent way to cut through hype... but have you tried running a benchmark yourself? It should be straightforward enough, right? You'd expect simple tools for the job. *Sighs.*

Yeah, that's what I thought too. Until I met `lm-evaluation-harness`, the cause of all suffering.

`lm-evaluation-harness` promises to make benchmarking straightforward and reliable. Instead, it hits you with configuration options so stupid they make you want to die.

I didn't want to create [an alternative](https://github.com/ToxicPine/easybench), I _had_ to.

## WTF?

Okay, let's be fair for a moment. The *intention* behind `lm-evaluation-harness` seems noble: simplify the process of implementing new benchmarks by taking coding out of the user's hands. The idea is to treat benchmark definitions purely as *configuration files* – collections of data (usually in YAML) that instruct the main evaluation program on how to behave, without requiring the user to write Python logic for each specific benchmark.

Theory: simple. Reality: spectacular failure.

Just glance at the sheer volume of *stuff* you need to understand just to use this "simple" configuration format:

- What's the difference between `dataset_path` and `dataset_name`? 
- How does `doc_to_text` find variables like `{{question}}`? 
- What Jinja syntax (`{% raw %}{% if %}{% endraw %}`) is allowed inside that YAML string? 
- What hidden Python function does `!function utils.helper` call? 
- Which `filter` functions (`regex`, `take_first`, `remove_whitespace`) exist, and what are their exact arguments inside nested YAML lists? 
- What does `metric: exact_match` *actually* calculate when combined with `aggregation: mean`, `higher_is_better: true`, and `regexes_to_ignore: [" "]`? 
- How do `generation_kwargs` like `until` interact with the base model settings? 

... and, most importantly: **why are there 30+ YAML provided for the `longbench` benchmark?**

Feeling overwhelmed? *Exactly*. This isn't configuration; it's psychic abuse disguised as not having to write code.

## A Taste Of Hell

I know what you're thinking: "yeah, but what _actually_ happens when you try to add a simple benchmark to `lm-evaluation-harness`? It can't be that hard, no?" *cue hysterical laughter*

I randomly selected an example benchmark. This was my warm welcome:

```yaml
# mgsm_direct_eu.yaml
{% raw %}doc_to_text: '{% if answer is not none %}{{question+"\nErantzuna:"}}{% else %}{{"Galdera: "+question+"\nErantzuna:"}}{% endif %}'{% endraw %}
```

Ahh... suffering. Oh, and where do "answer" and "question" actually come from?

1. It's defining `doc_to_text` (because "question_formatter" would be too intuitive)
2. Inside: Jinja templating (??) with `{% raw %}{% if %}{% endraw %}` conditional logic
3. Nested deeper: Variable interpolation using `{{}}` syntax
4. Even deeper: String concatenation operations
5. All of this: Crammed inside a YAML string

Yeah, easier than just writing Python? I don't think so.

Now, here's how we extract answers:

```yaml
filter_list:
{% raw %}  - name: flexible-extract
    filter:
    - function: regex
      group_select: -1
      regex_pattern: (-?[0-9]+([ .,][0-9.,]+)?)
    - function: take_first{% endraw %}
```

So now I need to:
1. Know that `filter_list` somehow post-processes model outputs
2. Guess which internal functions exist (documentation? what's that?)
3. Decipher cryptic parameters like `group_select: -1`
4. WTF is `take_first`?
5. ???

Want to configure metrics? Prepare for this beauty:

```yaml
metric_list:
{% raw %}  - metric: exact_match
    aggregation: mean
    higher_is_better: true
    ignore_case: true
    ignore_punctuation: true
    regexes_to_ignore:
      - " "{% endraw %}
```

What does `regexes_to_ignore: [" "]` actually do? Does it ignore spaces when comparing? Or is it ignoring regex patterns that consist of just a space? IS IT IGNORING MY WILL TO LIVE?

Need custom logic? Enter the dreaded `!function` escape hatch:

```yaml
{% raw %}doc_to_text: !function utils.format_basque_prompt{% endraw %}
```

WHERE IS THIS DEFINED? WHAT ARGUMENTS DOES IT TAKE? WHAT DOES IT RETURN?

Want simple parameter variations? TOO BAD! You MUST entire YAML files for each tiny change. That's why `longbench` has 30+ nearly identical files and why `gpqa` resembles a fractal nightmare of subdirectories.

Debugging this hellscape? When something breaks, you get helpful error messages like:

```
AttributeError: 'NoneType' object has no attribute 'group'
```

WHERE did this happen? In your YAML? In a template? IN THE FABRIC OF REALITY ITSELF?

## Something, Something, Abstraction

`lm-evaluation-harness` tries to simplify benchmarking by hiding the complex parts behind what *should* be a simple set of user-facing controls (an "abstraction"), but it fails. Instead of making things easier, its confusing system makes evaluating models *more* complicated.

**Good Abstraction:** A great example is Python's built-in `len()` function. You use `len("abc")` for strings, `len([1, 2, 3])` for lists, and `len({'key': 'value'})` for dictionaries. `len()` is a good abstraction because it provides a single command for the conceptually identical operation of "getting the size" across different data types. This simplifies your code by allowing you to ignore the specific implementation details of how counting works for each type of data, you just call `len()` where needed.

**Bad Abstraction:** `lm-evaluation-harness` often creates bad abstractions. It tries to force fundamentally different operations — like loading data, formatting a prompt, filtering output, and calculating a score — into the same complex YAML-based configuration system. The YAML system was designed to prevent you from coding each distinct benchmarking step (loading data, formatting prompts, grading answers). Yet, these steps *vary wildly* between benchmarks – they were never similar enough for this rigid structure. That's why this abstraction was bound to fail. It forces confusing hacks like `!function` tags and embedded code snippets, making the entire process *more* complex, not less. This is bad abstraction: it adds complexity instead of hiding it.

`lm-eval` *tried* to standardize benchmarking, but in the wrong places and using awful abstractions.

## It's That Bad

This isn't just whining. This terrible garbage:

1.  Discourages newcomers from running or contributing benchmarks.
2.  Wastes our research time on decoding YAML rather than actually analyzing results.
3.  Creates opportunities for misconfiguration and possibly even incorrect results.
4.  Makes it hard to comprehend how *exactly* how a published score was generated.

## Why I Made EasyLLMBench

I built **EasyLLMBench** because I hated working with `lm-evaluation-harness`.

Instead of wrestling with `lm-eval`'s cryptic YAML and its hidden logic, imagine simply writing Python. That's the core idea behind **EasyLLMBench**. Forget trying to decipher obscure configuration tags or embedding code snippets where they don't belong. Implementing a benchmark becomes a familiar task: create a Python class and override six clearly defined methods: `load_dataset`, `parse_dataset`, `generate_answer`, `grade_answer`, `compute_metrics`, and `print_metrics`.

This structure naturally guides you to focus *only* on the essential logic unique to your benchmark. How do *you* need to fetch your data? What's the right way to format *your* prompt? How should *this specific* answer be graded? What metrics truly matter for *this evaluation*? You answer these questions using standard Python, leveraging the tools and libraries you already know.

Where `lm-eval` gets bogged down trying to handle everything (often poorly) – forcing rigid structures, fumbling universal tasks like state management, and bundling unrelated concerns like model inference code – EasyLLMBench takes a different path. It focuses exclusively on automating the genuinely universal, tedious parts of benchmarking: the complex asynchronous orchestration needed for parallel runs, reliable state management to save, load, and resume progress, and basic logging and error handling during runs.

Crucially, EasyLLMBench deliberately *delegates* model inference entirely back to you. There's no framework code dictating how you call an API, manage a local model, handle batching, or set parameters. That logic belongs cleanly within *your* `generate_answer` method, where it makes the most sense. This keeps the framework lean, focused, and decoupled, preventing the kind of entanglement and hidden assumptions that make `lm-eval` so brittle and opaque.

This philosophy extends to how data and variations are handled. `lm-eval` often forces your data into specific shapes (like the infamous `doc_to_X` pattern) and requires duplicating entire configuration files for minor experimental variations. EasyLLMBench throws these constraints away. It only asks that you provide Python functions matching the six core method signatures and that your data structures can be serialized (which Pydantic makes trivial). *How* you implement those methods is your business. You can load data from a CSV, a database, or a web API, etc. You can parse it into any Python object structure you define (Pydantic helps keep this clear and type-safe). You can call any model provider or local library using the methods you prefer. You can calculate metrics using whatever custom logic makes sense for your task. And if you need variations – different prompts, different few-shot examples, different model parameters? They're just parameters passed to your benchmark class's `__init__` method – simple, and absolutely no file duplication needed.

There will be opportunities to eliminate repetitive, common code between similar benchmarks. That's why EasyLLMBench also provides a library of *optional* helper functions and classes. For instance, if your benchmark uses a standard dataset format from Hugging Face, you might use a pre-built `create_dataset_loader` function to quickly generate the `load_dataset` logic for you. Crucially, these are *helpers*, not requirements. If your data source is unusual, or you need custom loading logic, you simply write your own Python code within the `load_dataset` method, completely ignoring the helpers.

Finally, EasyLLMBench tackles the problem of bad abstractions that plague `lm-eval` and make useful standardization difficult. Instead of imposing one-size-fits-none concepts like `doc_to_X`, it embraces Python's native tools for *optional*, *explicit* standardization. If *you* find value in standardizing a specific behavior (like Chain-of-Thought prompting or a specific output parsing method) across several *similar* benchmarks, you can define a standard Python `Protocol` (an interface) specifying the methods required for that behavior. Benchmarks that need this capability can then *choose* to implement that protocol (e.g., `class MyBenchmark(Benchmark, SupportsCOT): ...`), or if appropriate, inherit from a class that already implements the required methods. This approach leverages Python's strengths for creating clear, opt-in contracts between components, promoting reusability where it makes sense, without resorting to the forced abstractions that ultimately add more complexity than they hide.

## The Conclusion

`lm-evaluation-harness` is proof that the road to hell is paved with good intentions. It created a system that is complex, opaque, and actively hostile to the simple goal of evaluating AI models.

[EasyLLMBench](https://github.com/ToxicPine/easybench) proves there's a better way.