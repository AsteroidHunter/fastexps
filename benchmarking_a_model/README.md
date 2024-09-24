## How quickly can I benchmark a small language model?
### Things done/tried/notes:
- For the benchmark, I chose [ARC-AGI](https://arcprize.org/arc)
 - In hindsight, this was a poor choice due to the complexity of the benchmark and the 
   lack of reasonably quick, positive feedback loops
- For the model, I was initially playing with Mistral 7B but later switched to Phi-3.5
- Tried to format the data into a dataframe and tokenize it for fine-tuning 
 - Errors faced during tokenization due to the data structure
 - Beyond that, fine-tuning the way I was doing it wasn't the correct approach
- Formatted the data as strings with the grid pattern
- All Phi-3.5 models are quite finicky about the input structure
 - The mini and vision models essentially don't work if special `<|user|>` and 
   `<|Image|>` tokens aren't present
 - I couldn't try the MoE version due to the lack of compatibility of flash attention 
   with my machine
   - This was a huge time sink (~3 hours); initially I couldn't even download the vision 
     model (turns out, within `AutoModelForCausalLM`, `_attn_implementation="eager"` 
     works but `attn_implementation="eager"` does not).
   - [This](https://huggingface.co/qnguyen3/nanoLLaVA-1.5/discussions/4) workaround 
     solution and its variants don't seem to work.
- From the light testing performed, the base `Phi-3.5-mini-instruct` shows poor 
  in-context learning and one-shot performance on these problems. I tried different 
  ways of prompting the puzzles (as grids, grids with spaces between individual 
  numbers, and list of lists, and flattened lists).
- The base version of `Phi-3.5-vision-instruct` also cannot one-shot solve these problems
- [Given Ryan Greenblatt's approach](https://redwoodresearch.substack.com/p/getting-50-sota-on-arc-agi-with-gpt) using GPT-4o, expecting any decent performance 
  with one-shot accuracy from Phi-3.5 is naive (i.e., I severely underestimated the 
  amount of time it would take me to solve this problem)

Total time spent so far: 8.5 hours