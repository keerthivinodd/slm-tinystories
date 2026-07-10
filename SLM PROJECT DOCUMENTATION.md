## **What is a Language Model?**

A language model is a machine learning model that learns patterns in text to predict the next word or token based on the words that come before it. By learning these patterns from large collections of text, it can generate coherent sentences, answer questions, complete text, and perform many natural language processing tasks. Modern language models typically use Transformer architectures to capture long-range relationships between words.

## **Why "Small"?**

A Small Language Model (SLM) contains millions of parameters instead of the billions found in large language models. It is trained on a focused, relatively simple dataset, allowing it to fit on a single consumer-grade GPU and complete training within a few hours rather than several weeks. This makes SLMs ideal for experimentation, education, research, and deployment on resource-constrained hardware.

## **Why TinyStories?**

TinyStories is a dataset containing approximately two million short, simple stories written using vocabulary that a three to four-year-old child can understand. It was specifically designed to demonstrate that small language models can still learn grammar, reasoning, and coherent text generation when trained on carefully curated data. The dataset was introduced by Eldan and Li (2023) in *TinyStories: How Small Can Language Models Be and Still Speak Coherent English?* (arXiv:2305.07759).

## **Pipeline Stages**

The SLM training pipeline begins by loading the raw text dataset and converting it into numerical subword token IDs using a tokenizer. These tokenized sequences are stored as efficient binary files and loaded in batches during training. The batches are then fed into a Transformer model, which is optimized using cross-entropy loss to predict the next token. After training, the model is evaluated on a separate validation dataset to measure performance, and finally it generates new stories from a user-provided prompt to demonstrate what it has learned.

### **Dataset**

The model is trained using the **TinyStories** dataset, which consists of simple, short stories written using basic English vocabulary. This makes it an ideal dataset for training a Small Language Model (SLM) from scratch, as it allows the model to learn grammar, sentence structure, and storytelling patterns without requiring massive computational resources.

The dataset is divided into the following splits:

* **Training Set:** **2,119,719** text samples  
* **Validation Set:** **21,990** text samples

The training split is used to teach the model to predict the next token in a sequence, while the validation split is used during training to evaluate the model's performance and monitor for overfitting. Together, these splits provide sufficient data for training and assessing the language model effectively.

### **Example from the TinyStories Dataset**

The following is an example of a story from the TinyStories dataset used to train the Small Language Model:

One day, a little girl named Lily found a needle in her room. She knew it was difficult to play with it because it was sharp. Lily wanted to share the needle with her mom, so she could sew a button on her shirt.

Lily went to her mom and said, "Mom, I found this needle. Can you share it with me and sew my shirt?" Her mom smiled and said, "Yes, Lily, we can share the needle and fix your shirt."

Together, they shared the needle and sewed the button on Lily's shirt. It was not difficult for them because they were sharing and helping each other. After they finished, Lily thanked her mom for sharing the needle and fixing her shirt. They both felt happy because they had shared and worked together.

### **Design Decisions**

Although the TinyStories dataset contains **2,119,719** training stories, only a subset of **200,000** training samples and **2,000** validation samples was used for this project. This was done to ensure that the model could be tokenized, trained, and evaluated within the three-day project timeline while using consumer-grade hardware.

Training on the entire dataset would require significantly more processing time, storage, and computational resources. A subset of 200,000 stories is still large enough for a Small Language Model (SLM) to learn fundamental language patterns, grammar, sentence structure, and simple storytelling, making it a practical balance between model quality and training efficiency.

**Subset Used:**

* Training Set: **200,000** stories  
* Validation Set: **2,000** storieS

### **Tokenized Dataset**

After preprocessing and tokenization, the dataset was converted into binary files for efficient loading during training. The resulting files contain the following number of tokens:

* **Training File (train.bin)**  
  * **44,970,964 tokens**  
  * **89.9 MB**  
* **Validation File (val.bin)**  
  * **389,121 tokens**  
  * **0.8 MB**  
    

### **Model Architecture**

The Small Language Model (SLM) used in this project is a transformer-based neural network designed for next-token prediction. It was configured to be compact enough to train on consumer-grade GPU hardware while still having sufficient capacity to learn language patterns from the TinyStories dataset.

**Model Details:**

* **Architecture:** Transformer-based Small Language Model (SLM)  
* **Total Parameters:** **49,343,232**  
* **Training Device:** **CUDA (GPU)**

The model contains **49,343,232 trainable parameters**, allowing it to capture grammar, sentence structure, and simple storytelling patterns while remaining significantly smaller than modern large language models. Training was performed on a **CUDA-enabled GPU**, providing much faster computation compared to CPU-based training.

### **Experiments**

Three different text generation settings were tested by varying the **temperature** and **top\_k** sampling parameters. With **temperature \= 0.5** and **top\_k \= 10**, the generated story was grammatically correct and coherent, but it was repetitive, with phrases such as "little girl named Lily" appearing multiple times. This setting produces safer and more predictable text because it restricts the model to choosing from the most likely next words.

Using **temperature \= 0.8** and **top\_k \= 50** resulted in more diverse and creative output. The story remained mostly grammatical and interesting, although it occasionally produced illogical events, such as hearing "a smoke" or going "inside the sink." This demonstrates the trade-off between creativity and consistency.

With **temperature \= 1.2** and **no top\_k restriction**, the output became highly random and largely incoherent. The generated text contained broken words, nonsensical phrases, and grammatical errors, making the story difficult to understand. The higher temperature increased randomness to the point where the model frequently selected unlikely tokens.

Overall, **temperature \= 0.8** with **top\_k \= 50** produced the best-quality stories. It provided a good balance between creativity and coherence, generating stories that were more varied than the low-temperature setting while remaining significantly more readable and grammatically correct than the high-temperature, unrestricted sampling approach.

