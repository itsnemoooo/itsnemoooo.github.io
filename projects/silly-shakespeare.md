---
layout: default

---

# TinyShakespeare GPT
**December 2024**  
*London, UK*

---

### Exploring transformers through the lens of poorly-written prose & verse.

the code is available [here](https://github.com/itsnemoooo/gpt-scratch).

transformers have **reshaped the field of NLP**, and even small experiments can unlock profound insights into their power.


a sample of that power is below. Let's hear from the model, trained entirely locally on the tiny shakespeare dataset:

```
And bid me with and man's time his heart shall be not;
For, you have warr'd honour is my labour his or no;
Thy wit; whose mides may charge fair ho go to-day,
A marblinshment of itself?

VIRARGILIA:
And most rain in physicanion,
And within penetents to llay limbs wooise,
That crossly doth stin threshe diety sent mels
Shall sun: 'ear he; and where he wild ...
```
not bad Shakespeare, not bad.
<div style="text-align: center;">
    <img src="/assets/images/tipsyshakespeare.png" alt="Figure 1: TinyShakespeare" width="200" />
    <p><em>Figure 1: DALL·E "A cartoon depiction of a middle-aged man with a receding hairline, a pointy beard, wearing an earring and a ruff."</em></p>
</div>

---
## 1. the dataset: tiny yet mighty
the Tiny Shakespeare dataset, a compact collection of the Bard’s works, is ideal for experimenting with NLP without incurring heavy computational costs.

key challenges included:
- **Limited Data:** Small datasets demand careful model tuning to prevent overfitting.
- **Character-Level Modeling:** At the character level, sequences are longer and less semantically dense than word-based models, making it challenging to capture meaningful patterns.

---

## 2. decoder-only transformer: a simplified architecture
unlike full transformer architectures, which include both encoder and decoder stacks, *TinyShakespeare* is a **decoder-only model**. This setup is optimized for autoregressive tasks, in this case text generation, where each token is predicted based on prior tokens in the sequence.

if you are familiar with the paper, Attention is All You Need, you will know that the decoder-only transformer is a simplified version of the full transformer architecture pictured below:

<div style="text-align: center;">
    <img src="/assets/images/attn.png" alt="Figure 2: Transformer" width="1000" />
    <p><em>Figure 2: Transformer</em></p>
</div>

I have plastered over the pieces that are not relavent to our decoder-only transformer.

---

## 3. before the transformer

#### **preparing data for transformer (1). embedding choice**
we first found the vocabulary span of the dataset to be 65 unique characters.
```python
chars = sorted(list(set(text)))
vocab_size = len(chars)
```
then built a mapping from tokens to integers, on the character level.
```python
stoi = { ch:i for i,ch in enumerate(chars) }
itos = { i:ch for i,ch in enumerate(chars) }
encode = lambda s: [stoi[c] for c in s]
decode = lambda l: ''.join([itos[i] for i in l])
```
*we could also use sentencepiece, tiktoken or other tokenizers to get a more compact vocabulary. This would lead to a larger sequences, there is a trade off between sequence length and vocabulary size.*


we used this to create the data tensor -> separated the data into train (90%) and val (10%).

#### **preparing data for transformer (2). sampling data & context length**
we never feed all data in at once.

we work with chunks, sampled randomly from train dataset. They have a max length of block_size.

we want the transformer to learn to predict the next token- e.g. a a sample of **9** will produce **8** individual examples:
1. **Input Sequence**: 
   - Given a sequence of tokens: 
   ```
   [0, 1, 2, 3, 4, 5, 6, 7, 8]
   ```

2. **Prediction Steps**:
   - Step 1: Given `[0]`, predict `1`
   ```
   Input: [0]  ->  Output: [1]
   ```

   - Step 2: Given `[0, 1]`, predict `2`
   ```
   Input: [0, 1]  ->  Output: [2]
   ```

   - Step 3: Given `[0, 1, 2]`, predict `3`
   ```
   Input: [0, 1, 2]  ->  Output: [3]
   ```

   - Step 4: Continue this process until the block size is reached.

#### **preparing data for transformer (3). batching for train and target**
'batch_size' is how many independent sequences we want to process in parallel.
we stack them up into a tensor of shape (batch_size, sequence_length). with batch_size = 4 and sequence_length = 8:

inputs:
```
torch.size([4, 8])
tensor([[0, 1, 2, 3, 4, 5, 6, 7],
        [8, 9, 10, 11, 12, 13, 14, 15],
        [16, 17, 18, 19, 20, 21, 22, 23],
        [24, 25, 26, 27, 28, 29, 30, 31]])
```

targets:
```
torch.size([4, 8])
tensor([[1, 2, 3, 4, 5, 6, 7, 8],
        [9, 10, 11, 12, 13, 14, 15, 16],
        [17, 18, 19, 20, 21, 22, 23, 24],
        [25, 26, 27, 28, 29, 30, 31, 32]])
```
note how the targets are the inputs shifted by one position. This 4 x 8 array contains 32 examples since we can pass in context and validate with the target array.


#### **positional encoding**
this is a encoding layer that injects sequence information. We know the order of the tokens so we add a positional encoding to the input.

**toy example - bigram output:**

the model predicted the following

```
An.
NADin h'st aliva t orin I, latesu sindooorif
Miterefonee lde wiouteanay T: wite:

N athis aneas witolllutheree r ceasplind the:
M:
```
not very good at all... (code and steps are in bigram-ex.ipynb up to this point).

---

## 4. inside the transformer

make sure you get the shape of the input and output tensors right.

select a embedding, or channel dimension (C). for example 32.

select the number of heads we'd like, for example 4.

that will define the size of the heads. In that case 32 / 4 = 8 and each attention head will operate on an 8 dimensional vector.

as a reminder: B, T, C = batch size, sequence length, channel dimension (# of features or dimensions at each timestep)


#### **transformer block**
**'K'** being the key, **'Q'** being the query and **'V'** being the value

this is the core class. 

for a reminder, the transformer is pictured below:

<div style="text-align: center;">
    <img src="/assets/images/attn.png" alt="Figure 2: Transformer" width="400" />
</div>

it is the light gray box with the 'Nx' next to it, containing the multi-head attention and feed-forward components.

#### **self-attention (scaled dot-product attention)**
attention is a communication medium. Think of it like a directed graph, where the nodes are the tokens and the edges are the attention weights. It is useful but there is no notion of space, the nodes don't know where they are in the sequence. 


#### **multi-head attention**
apply multiple attentions in parallel and concat the results (over the channel dimension). It allows for attending to parts of the sequence differently (e.g. long-term / short-termdependencies).
<div style="text-align: center;">
    <img src="/assets/images/multi-attn.png" alt="Figure 3: Multi-head attention" width="200" />
    <p><em>Figure 3: Multi-head attention</em></p>
</div>

#### **feed-forward**
a simple MLP with a non-linearity (ReLU) and some residual connections. It gives the model a chance to learn more complex patterns for the logits.

#### **layer normalization**
this is a simple normalization layer that normalizes the features (think unit variance across the row) to help with training. more info here: [layer normalization](https://pytorch.org/docs/stable/generated/torch.nn.LayerNorm.html).


#### **dropout**
randomly disables neurons during training, encouraging the model to generalise better.

#### **residual connections**
a simple way to stabilise training and enable the model to learn effectively. Start with a superhighway from the output to the input then over time the model learns to use the residual connections to learn the patterns.
<div style="text-align: center;">
    <img src="/assets/images/res.png" alt="Figure 4: Residual connections" width="400" />
    <p><em>Figure 4: Residual connections</em></p>
</div>

for more details on the residual connections, you can refer to the original [paper](https://arxiv.org/abs/1512.03385).

---

## 5. model training and performance
feel free to run the code in gpt.py to see the training and validation loss. I'd reccomend only if you have a GPU or MPS enabled device.
```
Using device: mps
10.788929 M parameters
step 0: train loss 4.2221, val loss 4.2306
step 500: train loss 1.7446, val loss 1.9068
step 1000: train loss 1.3929, val loss 1.5991
step 1500: train loss 1.2671, val loss 1.5291
step 2000: train loss 1.1881, val loss 1.5071
step 2500: train loss 1.1205, val loss 1.4973
step 3000: train loss 1.0733, val loss 1.4812
step 3500: train loss 1.0192, val loss 1.5134
step 4000: train loss 0.9599, val loss 1.5159
step 4500: train loss 0.9138, val loss 1.5430
step 4999: train loss 0.8590, val loss 1.5598
```
as we can see there is a bit of **overfitting**, but the output is starting to look like Shakespeare, if he was not at his best.

```
And bid me with and man's time his heart shall be not;
For, you have warr'd honour is my labour his or no;
Thy wit; whose mides may charge fair ho go to-day,
A marblinshment of itself?

VIRARGILIA:
And most rain in physicanion,
And within penetents to llay limbs wooise,
That crossly doth stin threshe diety sent mels
Shall sun: 'ear he; and where he wild ...
```

this is the current end of the experiment for me as I have gotten a chance to build transformers and deepen my understanding of at least one half of the architecture.

I may extend this experiment in the future, but for now I'd like to thank the [karpathy blog](https://karpathy.ai/zero-to-hero.html) for providing a great resource to learn about transformers.

---

## 6. links
- [Attention is All You Need](https://arxiv.org/abs/1706.03762)
- [ChatGPT](https://openai.com/index/chatgpt/)
- [Language Models are Few-Shot Learners](https://arxiv.org/pdf/2005.14165)
- [Karpathy Blog](https://karpathy.ai/zero-to-hero.html)
- [Karpathy Video](https://www.youtube.com/watch?v=kCc8FmEb1nY&t=1271s)
- [Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/)
- [Residual Connections Paper](https://arxiv.org/abs/1512.03385)

