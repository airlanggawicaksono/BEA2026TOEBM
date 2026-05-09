This dataset is an extension of the original Knowledge-based Vocabulary Lists (https://www.britishcouncil.org/research-insight/knowledge-based-vocabulary-lists) developed by Schmitt et al. (2024), adapted for NLP applications by Skidmore et al. (2025).  

The dataset contains 6,768 unique English vocabulary test items, with prompts in three languages (L1s): Spanish, German and Mandarin Chinese, totalling 20,304 items. Here is an example test item in Spanish for the English target word 'house': 

casa	Vivo en una casa grande que tiene tres dormitorios.
h _ _ _ _


The dataset is divided into three CSV files, one for each L1: 
- kvl-spanish-extended-v1.00.csv 
- kvl-german-extended-v1.00.csv
- kvl-chinese-extended-v1.00.csv


Each file includes the following data columns:
- item_id: An id number from 1 to 6,768. Items with the same item_id across different L1 files are parallel (i.e., same English target word).
- subset: Indicates the data split — either 'train', 'dev', or 'test'. These splits reflect those used in the study by Skidmore et al. (2025).
- L1: The L1 used in the prompt ('es', 'de', or 'cn' for Spanish, German or Mandarin Chinese, respectively).
- en_target_word: The English target word being tested.
- en_target_pos: The part of speech of the English target word.
- en_target_clue: A partial-spelling clue of the English target word, provided to the test-taker (e.g., 'h _ _ _ _' for 'house').
- L1_source_word: The corresponding L1 source word(s) for the English target word, provided to the test-taker (e.g., 'casa' for 'house').
- L1_context: The L1 contextualising prompt containing the L1 source word, provided to the test-taker (e.g. 'Vivo en una casa grande que tiene tres dormitorios.') 
- GLMM_score: The raw difficulty estimate for the vocabulary test item, calculated separately for each L1 using a random-item random-person (RPRI) Rasch model implemented within a generalised linear mixed model (GLMM) framework (see Schmitt et al. 2024, for more detail).
- difficulty_value: A difficulty value between 0 and 1, derived by linearly scaling the inverse of the GLMM_score (see Skidmore et al. 2025, for more detail).


References
- Norbert Schmitt, Karen Dunn, Barry O’Sullivan, Laurence Anthony, and Benjamin Kremmel. 2024. Knowledge-based Vocabulary Lists. University of Toronto Press, Toronto. 
- Lucy Skidmore, Mariano Felice and Karen J. Dunn. 2025. Transformer Architectures for Vocabulary Test Item Difficulty Prediction. In Proceedings of the 20th Workshop on Innovative Use of NLP for Building Educational Applications (BEA 2025), Austria, Vienna. Association for Computational Linguistics.


License

This dataset is licensed under the Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0).
