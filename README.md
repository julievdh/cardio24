# cardio24
online diagnostic platform that lets one continuously monitor ECG

Software required: MATLAB

Cardio24 Matlab scripts:
  1. afib_check : Function that takes ECG signal as input and outputs the observed morphologies which would help to identify abnormal parts of the input ECG signal.
  2. afib_input : Function that takes ECG signal as a file (txt file) and Sample Frequency as inputs, passes this data to 'afib_check' function and stores the outputs in a file (csv/json file)  

Description of 'afib_check' Function: 

  This code is designed based on parameters of ECG signal (Fs, gain) given for MIT-BIH Database, PhysioNet. Adjust output parameters of this function based on need. 
  
  Inputs:
  
    1. Input_ECG : Row/Column vector of the ECG signal (flag can be adjusted in the code)
    2. Fs : Sampling Frequency of the ECG signal
    
  Outputs:
  
    1. x1 : Preprocessed ECG signal (DC subtracted, gain-reduced)
    2. N : Length of the ECG signal
    3. Morphs : 
        size: 1x12 vector 
        data: 12 Morphological values
              i.Max HR
              ii. Avg HR
              iii. Min HR
              iv. Total Number of QRS Complexes
              v. Number of Irregular Beats
              vi. Percentage of Irregular Beats
              vii.Number of Episodes with Consec Irregular Beats
              viii. Average PR Interval
              ix. Average QRS Interval
              x. Average QTc Interval
              xi.Number of P wave absences
              xii.Number of Episodes that has >4 consec P wave absences
    4. Morphs_c :
        size: 1x12 vector 
        data: Normal/Abnormal condition based on above morphologies respectively
              Morphs_c(1,i) = 'Normal' or 'Abnormal'
    5. time_markRint : 
        size: 1xN vector
        data: marks locations of Irregular Beats with HIGH/LOW. Here: 0.9/0
            time_markRint(1,i) = HIGH if Beat at 'i'th sample point is Irregular;Otherwise, LOW.
    6. time_RR :
       size: 1xN vector
       data: Array of Beat to Beat Intervals 
            time_RR(1,i) = Interval from Beat at 'i'th sample point to Beat at 'i+1'th sample point.
    7. P_abs : 
        size: 1xN vector
        data: marks locations of P wave absences with HIGH/LOW. Here: 0.3/0
    8. time_RR2:
        size: 1xN vector
        data: marks the episodes of consecutive irregular beats with value of R_peak. 
    9. R_loc:
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: locations of R peaks
    10. R_value:
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: values of R peaks
    11. S_loc:
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: locations of S peaks
    12. S_value:
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: values of S peaks
    13. Q_loc:
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: locations of Q peaks
    14. Q_value,
        size: 1xnQRS vector  (nQRS is number of observed QRS complexes )
        data: values of Q peaks
    15. T_loc:
        size: 1x(nQRS-1) vector  (nQRS is number of observed QRS complexes )
        data: locations of T peaks
    16. T_value:
        size: 1x(nQRS-1) vector  (nQRS is number of observed QRS complexes )
        data: values of T peaks
    17. P_loc:
        size: 1x(nQRS-1) vector  (nQRS is number of observed QRS complexes )
        data: locations of P peaks
    18. P_value:
        size: 1x(nQRS-1) vector  (nQRS is number of observed QRS complexes )
        data: values of P peaks

Resources:
  1. ECG Data

      i) Physionet ATM Toolkit :  https://physionet.org/cgi-bin/atm/ATM. This code is tested on 1 hour ECG signals from  MIT-BIH Arrhythmia Database and QT Database
  
Results:

![alt tag](https://f13e59e9-a-62cb3a1a-s-sites.googlegroups.com/site/harshavardhaniitg/projects/cardio24_data/PQRST_Det.png?attachauth=ANoY7coQpXEE_PIAfaZeZ_V78Rzpe0P2OOXg5kdowU2HCnUGL6dkcDksfW7wBrB_kcIDPU4Ail4Lo6DD0bzywt96KCZ5E7rwHAgD6jR56wCDelpte736ZAR-CDLzrjMa15TGi76u4dTKbkc74hGfuLkL02MUd9sHsSCF8DkZyDSWU4hsfP7U0Dur_GNtcxHzpBroJ6Kq1_kdjz9EC8noqJD3YBWYts_nkS3Gojsmfl-YdSI_DNi-3CEv1CxR-PsSgx1PSrjrx7KJ&attredirects=0)
