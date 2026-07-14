**Objective**

This project implements a decoder-only Transformer Language Model (GPT-style) from scratch and trains it on the TinyStories dataset. The project covers the complete language model pipeline, including data preprocessing, Byte Pair Encoding (BPE) tokenization, Transformer architecture implementation, model training, evaluation, and text generation.

**Dataset**
Dataset: TinyStories (roneneldan/TinyStories) from Hugging Face
Original Dataset Size:
Training: 2,119,719 stories
Validation: 21,990 stories
Subset Used for Training:
Training: 200,000 stories
Validation: 2,000 stories

The subset was selected to reduce training time while still providing enough data to learn coherent language generation within the project timeline.

**Tokenization**

The text was tokenized using Byte Pair Encoding (BPE) through the tiktoken library with the GPT-2 vocabulary.

Vocabulary size: 50,257 tokens
Storage format: Memory-mapped binary (uint16)
Efficient random-access loading during training
Token Statistics
File	Tokens	Size
train.bin	44,970,964	89.9 MB
val.bin	389,121	0.8 MB

**Model Architecture**

A decoder-only Transformer inspired by GPT.

Configuration
Transformer Blocks: 6
Attention Heads: 6
Embedding Dimension: 384
Context Window (Block Size): 256
Vocabulary Size: 50,257
Total Parameters: 49,343,232
Components
Token Embeddings
Positional Embeddings
Multi-Head Causal Self-Attention
Feed Forward Network (MLP)
Residual Connections
Layer Normalization
Linear Language Modeling Head



**Training**
Hyperparameters
Parameter	Value
Optimizer	AdamW
Learning Rate	3e-4
Weight Decay	0.1
Batch Size	32
Block Size	256
Training Iterations	3000
Hardware	Google Colab T4 GPU
**Final Performance**
Metric	Value
Validation Loss	2.4170
Perplexity	11.21

The decreasing validation loss throughout training indicates that the model successfully learned meaningful language patterns from the TinyStories dataset while maintaining good generalization.

**
Sample Generations**
Sample 1

Once upon a time there was a little rabbit who loved to play in the forest. One day she found a beautiful flower. She picked it carefully and gave it to her mother. Her mother smiled and thanked her for being kind. The rabbit felt happy because sharing made everyone smile.

Sample 2

Tom wanted to build a small tower with blocks. At first it kept falling down, but he did not give up. He tried again and stacked each block carefully. Soon he had the tallest tower he had ever made. Tom learned that patience helps us succeed.

Sample 3

A little bird was afraid to fly across the river. Its father stayed beside it and encouraged it to keep trying. After a few small flaps, the bird reached the other side safely. It chirped happily and thanked its father for believing in it.

**Experiments: Sampling Strategy Comparison
**
Different sampling parameters were tested to observe how they affected the generated stories.

Temperature	Top-k	Observation
0.5	10	Produced the most coherent and grammatically correct stories. Text was predictable but highly consistent.
0.8	20	Balanced creativity and coherence. Stories became more varied while remaining easy to understand.
1.0	None	Generated more diverse outputs, but grammatical errors and repetitive phrases appeared more frequently.

Overall, temperature = 0.5 and top-k = 10 produced the highest-quality stories. Lower temperature made the model more confident in selecting likely tokens, resulting in smoother grammar and stronger story structure.

**How to Reproduce**
Clone the repository.
git clone <repository-url>
cd <repository-name>
Open notebooks/slm_build.ipynb in Google Colab.
Select:
Runtime
→ Change runtime type
→ GPU
→ T4 GPU
Run all notebook cells sequentially.
After training completes, evaluate the model and generate sample stories.
References
Eldan, R., & Li, Y. (2023). TinyStories: How Small Can Language Models Be and Still Speak Coherent English? arXiv:2305.07759.
Andrej Karpathy. nanoGPT. GitHub Repository.
Hugging Face Datasets. TinyStories Dataset.
OpenAI. tiktoken Tokenizer.
Trained Model Checkpoint

The trained model checkpoint is hosted on Google Drive because it exceeds GitHub's file size limit.
