# Spekboom nanopore sequencing



## Setup computer

High accurate basecalling is VERY slow using a "normal" computer. Having access to a powefull GPU accelerates this significantly. 

We used this gaming laptop: 

**MSI GP66 Leopard 15.6" Gaming Laptop - Intel® Core™ i7, RTX 3080, 1 TB SSD**
 

1. Install Nvidia drivers
2. Install cuda drivers
	* [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads) 		
3. Install guppy
	* download from [nanoporetech.com](nanoporetech.com)
	 
	
	Note: *you need to be registered with Oxford Nanopore. 
	If you want access to this downlod area you have to have ordered a starter pack already.*  
	
	* Double-click on the downloaded file to start installer. That is something like `ont-guppy-6.3.8-win64.msi`. Follow instructions.
4. Open windows command prompt and go into parent folder of location of raw data

	
	Note: *be careful about your data management. 
	Do not mix your new basecalls with the rawdata you get from the sequencers. 
	We decided to keep every flow cell run in a separate folder. 
	Folder name starts with date and follows with _FC and flowcell number with respect to the spekboom project.*
	



	

5. Run the guppy command
	
	Note: *be aware of spaces in windows folder names. Use double quotes around commands!*
	
	* find out, which config file you need. Run the `guppy_basecaller.exe` with option `--print_workflows`. Find your the flow cell and kit you have been using and use the listed config name for command below. The ending of that config file defines the accuracy of your basecalling. "hac" stands for high accuracy, for example.
	
	
	Now, run the actuall basecalling.
	
	
	```
	"C:\Program Files\OxfordNanopore\ont-guppy\bin\guppy_basecaller.exe" --config dna_r9.4.1_450bps_hac.cfg -i . --save_path . --device "cuda:0" -r --compress_fastq
	```

	* The ending of the config file defines basecalling mode. fast, hac (high accuracy) and sup (super accurate)
	* `-r` means recursively going through all fast5 files in the subfolder structure.
	* `--compress_fastq` gives gzip files rather than uncompressed fastq. 
	* `--device "cuda:0"` activates GPU. Check in Task manager if your graphics card is actually in use. 
 	

		

	
