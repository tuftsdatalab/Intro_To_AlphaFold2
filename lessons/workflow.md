* intro to navigating with HPC/copy data directory with alphafold outputs
  * questions:
  * How many models were created
  * Which file type contains the model's pLDDT information 
* plot with script: 
  * questions: 
  * How many Sequences were used in the PNCA msa and the LIG1 msa?
  * At which residue do the confidence scores drop off for PNCA and LIG1?
  * Given the MSA Plot do the majority of the sequences have a sequence identity above 90%(0.9)?
```
module load alphafold/2.1.1
python3 vizaf2.py --input_dir ./lig1/1X9N/ --output_dir ./lig1/visuals/ --name prefix
```
* plot/align with PyMOL
  * questions: 
  * do the structures align well?
  * which alignment is worse? 
  * What would you suspect causes a worse alignment?
