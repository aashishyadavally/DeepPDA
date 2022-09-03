# (Partial) Program Dependence Learning
Code fragments from developer forums often migrate to applications due to the code reuse practice. Owing to the incomplete nature of such code fragments, analyzing them to early determine the presence of potential vulnerabilities is challenging. In this work, we introduce DeepPDA, a neural network-based program dependence analysis (PDA) tool for both complete and partial programs. We design DeepPDA to efficiently incorporate intra-statement and inter-statement contextual features into statement representations, thereby modeling PDA as a statement-pair dependence decoding task. Our empirical evaluation shows that DeepPDA predicts the CFG and PDG edges in complete Java and C/C++ code with combined F-scores of 94.29% and 92.46%, respectively. The F-scores for partial Java and C/C++ code range from 94.29%–97.17% and 92.46%–96.01%, respectively. We also test the usefulness of the PDGs predicted by DeepPDA (PDG\*) on the task of method-level vulnerability detection (VD). We discover that the performance of the VD tool utilizing PDG* is only 1.1% less than that utilizing the PDGs generated by a program analysis tool. Furthermore, we report the detection of 14 real-world vulnerable code snippets from StackOverflow by a machine learning-based VD tool that employs the PDGs predicted by DeepPDA for these code snippets.


### Model Architecture for DeepPDA
<p align="center">
<img width="750" height="250" src="https://github.com/deeppda-icse23/DeepPDA/blob/main/figures/architecture.jpg">
</p>


### Dataset Links
Here are the links for datasets used in this paper:
  1. Java dataset for intrinsic evaluation: [link](https://drive.google.com/drive/folders/1WQQEmE6xpPD-fZBBxf0-4VFy-msVeh1O?usp=sharing)
  2. C/C++ dataset for intrinsic evaluation: [link](https://drive.google.com/drive/folders/1Vwrk4cFYpjB_C0FSIFmPX89cPFCtm1QB?usp=sharing)
  3. Java dataset for method-level vulnerability detection: [link](https://drive.google.com/drive/folders/1LVlQJz4sXkByJS9FUW61ecSv_jWI75E_?usp=sharing)

### Run Instructions
  
```
$ python run.py [options]

Options:
  -h, --help            show this help message and exit
  --data_dir DATA_DIR   Path to datasets directory.
  --output_dir OUTPUT_DIR
                        The output directory where the model saves model checkpoints
  --lang {c,java}       Programming language.
  --expt_name EXPT_NAME
                        Name of experiment to log in Weights and Biases.
  --max_tokens MAX_TOKENS
                        Maximum number of tokens in a statement
  --max_stmts MAX_STMTS
                        Maxmimum number of statements
  --num_layers NUM_LAYERS
                        Number of layers for Transformer encoder
  --num_layers_stmt NUM_LAYERS_STMT
                        Number of layers for Self-Attention Network
  --forward_activation FORWARD_ACTIVATION
                        Non-linear activation function in encoder
  --hidden_size HIDDEN_SIZE
                        Hidden size of decoding MLP
  --intermediate_size INTERMEDIATE_SIZE
                        Dimensionality of feed-forward layer in Transformer
  --embedding_size EMBEDDING_SIZE
                        Dimensionality of encoder layers
  --num_heads NUM_HEADS
                        Number of attention heads
  --vocab_size VOCAB_SIZE
                        Vocabulary size
  --use_stmt_types      Use statement type information.
  --no_ssan             Do not use self-attention network for statement
                        encoding.
  --no_pe               Do not use statement-level position encoding.
  --no_tr               Do not use transformer encoder.
  --load_model_path LOAD_MODEL_PATH
                        Path to trained model: Should contain the .bin files
  --do_train            Whether to run training.
  --do_eval             Whether to run eval on the dev set.
  --do_eval_top_k       Whether to run eval on the partitioned dev set.
  --do_predict          Whether to predict on given dataset.
  --log_interval LOG_INTERVAL
  --train_batch_size TRAIN_BATCH_SIZE
                        Batch size per GPU/CPU for training.
  --eval_batch_size EVAL_BATCH_SIZE
                        Batch size per GPU/CPU for evaluation.
  --learning_rate LEARNING_RATE
                        The initial learning rate for Adam.
  --weight_decay WEIGHT_DECAY
                        Weight deay if we apply some.
  --dropout_rate DROPOUT_RATE
                        Dropout rate.
  --adam_epsilon ADAM_EPSILON
                        Epsilon for Adam optimizer.
  --num_train_epochs NUM_TRAIN_EPOCHS
                        Total number of training epochs to perform.
  --seed SEED           random seed for initialization

``` 

### Sample Run Command:
```bash
$ python run.py --data_dir ./datasets/ --output_dir ./outputs/intrinsic/java_8 --lang java --do_train --use_stmt_types --max_stmts 8 --expt_name intrinsic-java-8
```
