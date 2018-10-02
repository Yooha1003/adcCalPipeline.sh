# adcCalPipeline.sh

Pipeline script for calculating adc values from an anatomical image registered dwi image


----------------------------------------------------------------------------------------------------
  Description:\
    This script is for calculation of ADC values using fslmaths commands.\
    This script is a whole pipeline with four main steps for reconstruction of ADC maps.\
      Step 1. Gradient correction using HCP 'gradient_unwarp.py' script\
      Step 2. Distortion and Eddy current and motion correction for dwi and epi images\
              (https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/eddy/UsersGuide)\
      Step 3. Transformation between [DWI/EPI] and T1w image\
      Step 4. ADC calculation with aligned DWI images\
    The script requires a specific data acquisition method (see the 'Requirement' section).

  Development History:\
    Version 0.24 : Bug fixed with a file summary and re-naming b1/b2 values (2018.10.1)\
    Version 0.23 : threshold adc map (value = 5000) (2018.9.28)\
    Version 0.22 : Bug fixed (resampling problem / hyper-voxel of ADC removal) (2018.9.28)\
    Version 0.21 : Added reconstruction of dwi images with different b-values (2018.9.21)\
    Version 0.2  : Added 'SLOT' system for a flexible input analysis (2018.9.21)\
    Version 0.1  : Release Script (2018.9.19)\

----------------------------------------------------------------------------------------------------
  Example Usage:
  adcCalPipeline.sh -f file_list.txt -t readout_time.txt -g coeff.grad -a bval1 -b bval2

  (Optional)
  adcCalPipeline.sh -ver (see the version)

  Compulsory arguments:\
      -f:  image names with a fixed order (see more details in 'Requirement' section)\
      -t:  readout time list (calculated by our in-house excel file)\
      -g:  gradient file from Siemens console\
      -a:  1st b-value\
      -b:  2nd b-value\
      
----------------------------------------------------------------------------------------------------

Requirement:\
    1. MP2RAGE sequence images (INV1/INV2/T1/UNI) / TSE image / DWI images / (optional) EPI images\
    2. Python 2.7 installation\
    3. gradunwarp installation (HCP pipeline script) / gdc.sh (in-house script)\
    4. FSL installation (and eddy_cpu binary file from 5.0.11 patch)\
    5. ANTs installation\
    6. Data file name list without any extension (6 SLOTs supported)\
      1)  [Mandatory] INV1 (MP2RAGE)\
      2)  [Mandatory] INV2 (MP2RAGE)\
      3)  [Mandatory] UNI (MP2RAGE)\
      4)  [Mandatory] T1 (MP2RAGE)\
      5)  [Mandatory] TSE (Turbo Spin Echo)\
      6)  [Mandatory] PA (DWI)\
      7)  [SLOT1] for DWI (if you want to skip this slop, input "0" in the text file)\
      8)  [SLOT2] for DWI (if you want to skip this slop, input "0" in the text file)\
      9)  [SLOT3] for DWI (if you want to skip this slop, input "0" in the text file)\
      10) [SLOT4] for DWI (if you want to skip this slop, input "0" in the text file)\
      11) [SLOT5] for EPI PA (if you want to skip this slop, input "0" in the text file)\
      12) [SLOT6] for EPI AP (if you want to skip this slop, input "0" in the text file)\
    7. Readout time list with a determined order (5 SLOTs supported)\
      1)  [TIME1] SLOT1 image readout time\
      2)  [TIME2] SLOT2 image readout time\
      3)  [TIME3] SLOT3 image readout time\
      4)  [TIME4] SLOT4 image readout time\
      5)  [TIME5] SLOT6 image readout time\
    8. fastSegASingle.sh (in-house script for MP2RAGE segmentation)\
    9. yhBrainExt.sh (in-house script for brain extraction, in case of an absence of UNI image)
    
---------------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------------

  This method was created by:

  Uksu, Choi (uschoi@nict.go.jp)
  Center for Information and Neural Networks
  National Institute of Information and Communications Technology
  
---------------------------------------------------------------------------------------------------
                      Script writing and modification by Uksu
                      Do not modify without a permission.
---------------------------------------------------------------------------------------------------

