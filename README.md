# Auto-Vicuna

## 0x1 Prerequisite

install [vicuna](https://github.com/lm-sys/FastChat)
model [example](https://huggingface.co/eachadea/vicuna-13b-1.1)

install Auto-GPT based on the DGdev91's PR #2594 (2023/04/22). You can do this by:

     git clone https://github.com/DGdev91/Auto-GPT.git # clone DGdev91's fork
     cd Auto-GPT
     git checkout b349f2144f4692de7adb9458a8888839f48bd95c # checkout the PR change

## 0x2 Guide
1. Start Fastchat API
```
python -m fastchat.serve.controller

python -m fastchat.serve.model_worker --model-name 'gpt-3.5-turbo' --model-path /path/to/vicuna/weights

export FASTCHAT_CONTROLLER_URL=http://localhost:21001
python3 -m fastchat.serve.api --host localhost --port 8000

# or windows powershell
$env:FASTCHAT_CONTROLLER_URL="http://localhost:21001"
python -m fastchat.serve.api --host localhost --port 8000
```
`--model-name` must be "gpt-3.5-turbo" for Auto-GPT :(   I don't know how to modify it.

2. modify `autogpt/llm_utils.py`
delete line 96, line 97 
```
    else:
        response = openai.ChatCompletion.create(
            model=model,
            messages=messages,
            temperature=0.9,
            max_tokens=3094,
        )
```
to
```
    else:
        response = openai.ChatCompletion.create(
            model=model,
            messages=messages,
        )
```
I don't know why, maybe fastchat not support temperature & max_tokens.

## todo

`Vicuna` may not be generate command to excute, maybe add more prompt.
