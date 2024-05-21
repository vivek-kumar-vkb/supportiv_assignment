# Supportiv_assignment

## Problem Statement
* We need to create a chatbot with Medical Question Answer Dataset
### Approach to the Problem:
* We will create an encoder/decoder model that will take the data that we provide and output our response using the techniques of machine translation.

## Below is the high level process of what we aim to do .


In place of Marathi words we want our model to output the answers to the question provided as input to the encoder.
**At a very high level, an encoder-decoder model can be thought of as two blocks, the encoder and the decoder connected by a vector which we will refer to as the ‘context vector’.**
* Encoder: The encoder processes each token in the input-sequence. It tries to cram all the information about the input-sequence into a vector of fixed length i.e. the ‘context vector’. After going through all the tokens, the encoder passes this vector onto the decoder.


* Context vector: The vector is built in such a way that it's expected to encapsulate the whole meaning of the input-sequence and help the decoder make accurate predictions. We will see later that this is the final internal states of our encoder block.
* Decoder: The decoder reads the context vector and tries to predict the target-sequence token by token.

## Assumptions made by our SEQ2SEQ Model:
1. Equal Importance of All Inputs: All tokens in the input sequence are treated equally, regardless of their position or relevance to the current decoding step. This means that the model does not explicitly prioritize certain parts of the input sequence over others during decoding.
2. Short-Term Dependencies: The model assumes that all relevant information needed to generate the output sequence is captured in the fixed-length representation obtained from the encoder. Therefore, it may struggle with capturing long-range dependencies or understanding context that spans across distant parts of the input sequence.
3. Context Compression: The fixed-length representation obtained from the encoder must compress all relevant information from the input sequence into a single vector. This means that important details from the input sequence may be lost or diluted in the encoding process.

## Model Performance:
* LOSS FUNCTION USED:-**SparseCategoricalCrossentropy** with masking layer to ignore the padding of 0 for maintaining uniform length.


## Metrics used to find validation accuracy:
* We compare the predicted sentence to the true sentene and try to find out the number of words correctly predicted as n_correct to the total nuumber of words in the sentence.
* Our accuracy come out to be =n_correct/n_total
Model performance is graphical shown in code file attached wrt number of epoch done.

## Strengths of our Model:
1. **Decent Performance on Simple Tasks**: For simple sequence-to-sequence tasks with relatively short input and output sequences and limited long-range dependencies, the model without attention can perform reasonably well. It can learn basic mappings between input and output sequences and generate coherent output.
2. **Ease of Training:** The absence of attention simplifies the training process, as there is no need to compute attention weights or handle complex alignment between input and output sequences.
3. **Less Susceptible to Overfitting**: The model without attention has fewer parameters and a simpler architecture, which can make it less susceptible to overfitting, especially when trained on small datasets.
## Weakness of our model:
1. **Limited Context Understanding**: The fixed-length representation obtained from the encoder compresses all information from the input sequence into a single vector. This can lead to information loss, especially for longer input sequences, and limit the model's ability to understand and capture the full context of the input.
2. **Difficulty with Long Sequences:** Without attention, the model struggles to handle long input sequences effectively. It may have difficulty capturing long-range dependencies and may focus more on recent parts of the input sequence, leading to suboptimal performance for tasks with long input sequences.
3. **Inability to Handle Variable-Length Sequences:** The model without attention assumes fixed-length input and output sequences, making it less flexible in handling variable-length input and output sequences. It requires padding or truncation of sequences to a fixed length, which can introduce unnecessary complexity and inefficiency.

## Potention Future improvements:
1. **Questions can be taken as input**: The questions were given implicitly it can also be done by taking input from user and then pass it into the print_conversation() function
1. **Attention Mechanism**: Introducing an attention mechanism allows the model to dynamically focus on different parts of the input sequence during decoding. This helps the model handle long-range dependencies and better capture the alignment between input and output sequences.
2. **Larger Hidden State Size:** Increasing the size of the hidden states in both the encoder and decoder can help the model learn more complex representations of the input and output sequences. Larger hidden states provide the model with more capacity to capture and represent the semantic meaning of the input sequence and generate accurate predictions for the output sequence.
3. **Model Ensembling:** Combining the predictions of multiple independently trained seq2seq models can help improve the overall performance and robustness of the system. Each model may have different strengths and weaknesses, and ensembling helps mitigate individual model biases and errors.
