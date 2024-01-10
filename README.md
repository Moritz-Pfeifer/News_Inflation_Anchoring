## News Inflation Anchoring 

The goal of this project is to study the impact news opintions on the Bank of England have on shaping inflation expectations. From a large data set of Financial Times articles on the bank of England, we build a training data set using chat-gpt that classifies sentences into negative, positive or other. We then train a llama-2 model on that dataset which we use to construct a time series of news opintions. This repository includes all our data, model and codes. 

### Using Llama-2 to Extract Financial Times Opinions on the Bank of England

This model fine-tunes Llama-2-7B on an instruction dataset of Financial Times News which detects journalists' opinions about the Bank of England. It can label sentences as either "positive", "negative" or "other". 

### Intended Use

The model is intended to be used for any analysis where the reputation, legitimacy and credibility of the Bank of England and its monetary policy plays a role. 

#### Performance

- Accuracy: 78%
- F1 Score: 0.78
- Precision: 0.78
- Recall: 0.78

### Usage

You can use these models in your own applications by leveraging the Hugging Face Transformers library. Below is a Python code snippet demonstrating how to load and inference with the FT-News classification model:

```python
from peft import AutoPeftModelForCausalLM
from transformers import AutoTokenizer, pipeline

# Load the model
model = AutoPeftModelForCausalLM.from_pretrained("Moritz-Pfeifer/financial-times-classification-llama-2-7b-v1.3")
tokenizer = AutoTokenizer.from_pretrained("Moritz-Pfeifer/financial-times-classification-llama-2-7b-v1.3")

# Create a prompt for the model 
def predict_text(test, model, tokenizer):
    prompt = f"""
            You are given an opinion about the Bank of England (BoE).
            Analyze the sentiment of the opinon about the reputation of the Bank of England (BoE) enclosed in square brackets,
            determine if it is positive, negative or other, and return the answer as the corresponding sentiment label
            "positive" or "negative". If the opinion is not related, return "other".

            [{test}] ="""
    pipe = pipeline(task="text-generation",
                        model=model,
                        tokenizer=tokenizer,
                        max_new_tokens = 1,
                        temperature = 0.1,
                       )
    result = pipe(prompt)
    answer = result[0]['generated_text'].split("=")[-1]
    # print(answer)
    if "positive" in answer.lower():
        return "positive"
    elif "negative" in answer.lower():
        return "negative"
    else:
      return "other"

# Use the model
input_text = 'The report, by Lord Justice Bingham, said the Bank failed to take appropriate action after receiving a series of warnings over many years that fraud was taking place at BCCI.'
predict_text(input_text, model, tokenizer)
```
