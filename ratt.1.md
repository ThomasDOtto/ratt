% RATT(1)
%
%

# NAME

ratt - genome annotation transfer

# SYNOPSIS

RATT_HOME=/path/to/RATT \\ \
**ratt** \\ \
{**-p**|**--prefix**} *result-prefix* \\ \
{**-t**|**--type**} *transfer-type* \\ \
[{**-r**|**--refseq**} *reference.fasta*] \\ \
*reference-annotation-directory*
*query.fasta*

# DESCRIPTION

**ratt** (Rapid Annotation Transfer Tool) conducts synteny-based annotation transfer to a given sequence.

# ARGUMENTS

## REQUIRED

*reference-annotation-directory*
:    The directory containing all the reference annotation files to be transferred to the query.
     These files must be in EMBL format.

*query.fasta*
:    The nucleotide sequence to which the reference annotations will be mapped.

**-p**, **--prefix** *result-prefix*
:	The prefix you wish to give to each result file.

**-t**, **--type** *transfer-type*
:	The following types can be used:

	**Assembly**
	:    transfer between different assemblies
	**Assembly.Repetitive**
	:    As before, but the genome is extremely repetitive.
		 This should only be run if the parameter **Assembly** misses too many annotation tags.
	**Strain**
	:	 Transfer between strains. Similarity is between 95-99%.
	**Strain.Repetitive**
	:    As before, but the genome is extremely repetitive.
	     This should only be run if the parameter **Strain** misses too many annotation tags.
	**Strain.Global**
	:    If your assembly doesn't have many gaps and rearrangements, this option might help.
	**Species**
	:    Transfer between species. Similarity is between 50-94%
	**Species.Repetitive**
	:    As before, but the genome is extremely repetitive.
         This should only be run if the parameter **Species** misses too many annotation tags.
	**Species.Global**
	:    As before, but if your assembly doesn't have many gaps and rearrangements, this option might help.
	**Multiple**
	:    When many annotated strains are used as a reference and you assume that the query genome has many insertions compared to them, this parameter will use the best regions of each reference strain to transfer tags.
	**Free**
	:    The user sets all **nucmer**(1) parameters individually.
	     These parameters must be specified via the following environment variables:

		**RATT_l**
		:    word size
		**RATT_minInd**
		:    identity cutoff
		**RATT_c**
		:    cluster size
		**RATT_g**
		:    max extend cluster
		**RATT_anchor**
		:    anchor choice
		**RATT_rearrange**
		:    rearrange
		
## OPTIONAL

**-r**, **--refseq** *reference.fasta*
:    Name of multi-fasta file containing the reference sequences corresponding to the EMBL annotation files.
     **IMPORTANT**: The fasta sequence header names must exactly match the corresponding EMBL annotation files.

# ENVIRONMENT

**RATT_HOME**
:    Path to the **ratt** source directory.
     This variable must be set for the program to function.

**RATT_CONFIG**
:    Path to a custom configuration file to use.
     As start codons and splice sites might vary between organisms, it will be necessary to generate a configuration file for your specific needs.
	 Example configuration files for bacteria or eukaryotes called *RATT.config_bac* and *RATT.config_euk* are provided with the program.

**RATT_VERBOSE**
:    If this variable is defined, **ratt** will report its invocations of external programs.

**RATT_DOTRANSLATION**
:    When this variable is set to *1*, **ratt** will include protein amino acid sequences in the output.

# SEE ALSO

**nucmer**(1)

RATT is published as:

Thomas D. Otto, Gary P. Dillon, Wim S. Degrave, Matthew Berriman; RATT: Rapid Annotation Transfer Tool. Nucleic Acids Res 2011; 39 (9): e57. doi: 10.1093/nar/gkq1268
