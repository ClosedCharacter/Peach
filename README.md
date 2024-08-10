<!-- header start -->
<!-- 200823 -->
<div style="width: auto; margin-left: auto; margin-right: auto">
<img src="./PeachGirl.png" alt="Peach" style="width: 100%; min-width: 400px; display: block; margin: auto;">
</div>
<!-- header end -->

# Peach-9B-8k-Roleplay

Peach-9B-8k-Roleplay is a chat large language model obtained by finetuning [01-ai/Yi-1.5-9B](https://huggingface.co/01-ai/Yi-1.5-9B) model on more than 100K conversations created through our data synthesis approach.

 🤗 <a href="https://huggingface.co/ClosedCharacter/Peach-9B-8k-Roleplay" target="_blank">HF Repo</a>
 
**Maybe The Best LLM with Small Parameters under 34B**

## How to start
The version of Transformers we are using is as follows, but a newer version may be available.
```
torch==1.13.1
gradio==3.50.2
transformers==4.37.2
```

Then run the following code to infer.

```python
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

model_name_or_path = "ClosedCharacter/Peach-9B-8k-Roleplay"
tokenizer = AutoTokenizer.from_pretrained(model_name_or_path, use_fast=True)
model = AutoModelForCausalLM.from_pretrained(
    model_name_or_path, torch_dtype=torch.bfloat16, 
    trust_remote_code=True, device_map="auto")
messages = [
    {"role": "system", "content": "你是黑丝御姐"},
    {"role": "user", "content": "你好，你是谁"},
]
input_ids = tokenizer.apply_chat_template(conversation=messages, tokenize=True, return_tensors="pt")
output = model.generate(
    inputs=input_ids.to("cuda"), 
    temperature=0.3, 
    top_p=0.5, 
    no_repeat_ngram_size=6,
    repetition_penalty=1.1,
    max_new_tokens=512)
print(tokenizer.decode(output[0]))

```

Or you can just use below code to run web demo.
```
python demo.py
```
## Benchmark
| Metric         | Value           |
|----------------|-----------------|
| MMLU (5-shot)  | 66.19    |
| CMMLU (5-shot) | 69.07    |


## Warning
All response are generated by AI and do not represent the views or opinions of the developers.

1. Despite having done rigorous filtering, due to the uncontrollability of LLM, our model may still generate **toxic, harmful, and NSFW** content.

2. Due to limitations in model parameters, the 9B model may perform poorly on mathematical tasks, coding tasks, and logical capabilities.

3. Our training data is capped at a maximum length of 8k, so excessively long conversation turns may result in a decline in the quality of responses.

4. We used bilingual Chinese-English data for training, so the model may not perform well on other low-resource languages.

5. The model may generate a significant amount of hallucinations, so it is recommended to use lower values for temperature and top_p parameters.


# Contact Us

**微信 / WeChat: Fungorum**

**邮箱 / E-mail: 1070193753@qq.com**

<img src="./Wechat.jpg" alt="Peach" style="width: 100%; min-width: 400px; display: block; margin: auto;">

