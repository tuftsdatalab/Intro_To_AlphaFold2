## AlphaFold Output

 - Here we predicted the structures of PCNA and LIG1. Let's examine the output by navigating to the PCNA output folder:
 
 ```
 cd af2Workshop/pcna/1AXC/
 ls 
 ```
 - You should see output that looks like the following:
 
 ```
  [tutln01@c1cmp048 1AXC]$ ls
features.pkl  ranked_1.pdb  ranked_4.pdb                  relaxed_model_2_multimer.pdb  relaxed_model_5_multimer.pdb  result_model_3_multimer.pkl  timings.json                    unrelaxed_model_3_multimer.pdb
msas          ranked_2.pdb  ranking_debug.json            relaxed_model_3_multimer.pdb  result_model_1_multimer.pkl   result_model_4_multimer.pkl  unrelaxed_model_1_multimer.pdb  unrelaxed_model_4_multimer.pdb
ranked_0.pdb  ranked_3.pdb  relaxed_model_1_multimer.pdb  relaxed_model_4_multimer.pdb  result_model_2_multimer.pkl   result_model_5_multimer.pkl  unrelaxed_model_2_multimer.pdb  unrelaxed_model_5_multimer.pdb
 ```
 
 - Where:
 
|File/Directory|Description|
|-|-|
|features.pkl|A pickle file w/ input feature NumPy arrays|
|msas|A directory containing the files describing the various genetic tool hits that were used to construct the input MSA.|
|unrelaxed_model_\*.pdb|A PDB file w/ predicted structure, exactly as outputted by the model|
|relaxed_model_\*.pdb|A PDB file w/ predicted structure, after performing an Amber relaxation procedure on the unrelaxed structure prediction|
|ranked_\*.pdb |A PDB file w/ relaxed predicted structures, after reordering by model confidence (using predicted LDDT (pLDDT) scores). ranked_1.pdb = highest confidence ranked_5.pdb = lowest confidence|
|ranking_debug.json|A JSON file w/pLDDT values used to perform the model ranking, and a mapping back to the original model names.|
|timings.json|A JSON file w/times taken to run each section of the AlphaFold pipeline.|
|result_model_\*.pkl| A pickle file w/ a nested dictionary of the various NumPy arrays directly produced by the model: StructureModule Output, Distograms, Per-residue pLDDT scores, predicted TMscore, predicted pairwise aligned errors |



 
Next: [PlaceHolderText](../lesson4/lesson4.md)

Previous: [Setup](../lesson2/lesson2.md)

