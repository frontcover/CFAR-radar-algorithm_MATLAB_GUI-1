Translated:
## 1. Content introduction
  &nbsp; &nbsp; &nbsp; &nbsp;Use the MATLAB GUI design platform to design a multi-algorithm radar one-dimensional constant false alarm detection CFAR visual interface. By selecting the noise type, target type, algorithm type, manually inputting relevant parameters, the noise waveform and target are visually displayed. Detected echo-detection threshold waveform diagram. Run cfar.m to call the GUI for parameter input and output.
  ![Insert image description here](https://img-blog.csdnimg.cn/20200513184019391.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjc5NTcz,size_16,color_FFFFFF,t_70)
## 2. Introduction to the principle
  &nbsp; &nbsp; &nbsp; &nbsp;Constant false alarm detection technology (CFAR) refers to a technology in which the radar system distinguishes the signal and noise output by the receiver to determine whether the target signal exists while maintaining a constant false alarm probability.
   &nbsp; &nbsp; &nbsp; &nbsp;Premise: Since there must be noise (including atmospheric noise, man-made noise, internal noise and clutter, etc.) in the output of the receiver, the signal is generally superimposed on the noise. This requires using detection technology to determine whether there is a target signal under the condition of noise or signal plus noise output by the receiver.  ![Insert image description here](https://img-blog.csdnimg.cn/20200513184019391.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjc5NTcz,size_16,color_FFFFFF,t_70)
     &nbsp; &nbsp; &nbsp; &nbsp;Error probability: Any form of judgment must have two error probabilities: discovery probability and false alarm probability. When there is a target echo signal at the output end of the receiver, the probability that there is a target is Pd, and the probability that there is no target is 1-Pad. When there is only noise at the receiver output, the probability that there is a target is Pfa. Since noise is a random variable, its characteristics can be expressed by the probability density function, so the signal plus noise is also a random variable.
   &nbsp; &nbsp; &nbsp; &nbsp; The specific process: the constant false alarm detector first processes the input noise and determines a threshold, and compares this threshold with the input signal. If the input signal exceeds this threshold, it is judged as There is a target, otherwise, it is judged as no target.
    &nbsp; &nbsp; &nbsp; &nbsp; Algorithm: ① Mean type CFRA: The core idea is to estimate the background power by averaging the sampled data within the reference window. CA-CFAR (unit average constant false alarm), GO-CFAR (maximum selection constant false alarm), and SO-CFAR (minimum selection constant false alarm) algorithms are the most classic mean CFAR algorithms.
       &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Background noise. OS-CFAR (Ordered Statistical Constant False Alarm) is its classic algorithm.
      
## 3. Implement functions
![Insert image description here](https://img-blog.csdnimg.cn/20200513175854839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjc5NTcz,size_16,color_FFFFFF,t_70)
The functions implemented are:

1. Type selection: ① Noise type: uniform background noise and clutter edge background noise. Uniform background noise is noise with a single power. Just enter noise power 2, noise length 2, and noise variance in the parameter input interface (noise power 1 and noise length 1 are disabled); clutter edge background noise is a combination of two different power noises. For combination, you need to input the power and length of noise 1 and noise 2 respectively, and the variance is shared by the two noises.
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; When selecting a single target, you only need to enter the signal-to-noise ratio and location of target 1 (other targets are disabled); when selecting multiple targets, you need to enter the signal-to-noise ratio and location of targets 1-4 respectively. When the noise type is clutter When there is edge background noise, it is also necessary to input the signal-to-noise ratio and position of the target near the edge of the clutter and within the clutter to facilitate distinction and comparison.
   &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Just choose one.

2. Generate noise & noise waveform: After completing the selection of noise type and input of noise parameters, click the Generate Noise button to generate a noise waveform, which is displayed in the lower left corner.

3. Parameter input: ① Noise power 1/2: noise power size, unit db, variable names db1, db2.
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; length 1), the variable names are shape1, shape2.
   &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Ratio, the variable name is SNR1/2/3/4/5/6.
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The target position needs to be less than the maximum noise length. The clutter edge position should be the junction of the two sections of noise. The position within the clutter should be within the clutter. The variable name is des1/2/3/4/5/6.
    &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
    &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Several units are not used as background clutter estimates, but are used as protection units, and the variable name is pro_N.
    &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
						 

4. Output results & echo-detection threshold relationship diagram: Generate noise, enter target parameters, select the algorithm, and click the output result button to get the echo-detection threshold relationship diagram on the right.

5. Export left/right pictures: Export and save the noise waveform diagram and echo-detection threshold relationship diagram respectively. The optional formats are jpg, png, bmp, and eps.

## 4. Operation examples
Select the noise type as "clutter edge background noise", the target type as multi-target, the algorithm type as CA-CFAR, and the parameter input as the default input (noise power 1/2: 20db, 30db; noise length 1/2: 100, 200 ;Noise variance: 200; Signal-to-noise ratio 1/2/3/4/5/6:15, 12, 8, 5, 5, 5; Target position 1/2/3/4, clutter edge position, clutter Internal position: 30, 40, 50, 60, 95, 120; number of units: 36; number of protection units: 2; false alarm probability: 0.001), the result is as shown in the figure below: ![Insert picture description here](https://img-blog.csdnimg.cn/20200513183948353.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjc5NTcz,size_16,color_FFFFFF,t_70) It can be seen from the echo-detection threshold diagram that This algorithm has good target detection performance in low-noise environments and achieves constant false alarm detection, but its detection performance drops significantly at the edge of clutter and within the clutter.
## 5. Algorithm and parameter analysis
Analysis of Algorithms:
CA-CFAR: Advantages: An algorithm with the lowest loss rate;
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
  GO-CFAR: Advantages: Reduce the probability of false alarms in clutter edge areas
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Disadvantages: multi-target masking
SO-CFAR: Advantages: Multi-target effects are improved;
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
  OS-CFAR: Advantages: Multi-target detection performance is very good;
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
  Parameter analysis:
  Number of detection units: Under the same signal-to-noise ratio, a CFAR with more detection units has a higher detection probability, but at the same time, the amount of calculation increases.
  False alarm probability: With the same number of detection units, the higher the false alarm probability, the higher the CFAR detection probability, but the number of false alarms also increases.
  Signal-to-noise ratio: As the signal-to-noise ratio continues to increase, the detection probability also increases.
  Number of protection units: If a protection unit is too large or too small, the detection probability will be reduced. A moderate number of protection units should be selected for different experiments.
## 6. Statement

This project is my secondary analysis and development based on other CFAR articles. The original address is: https://www.cnblogs.com/Mufasa/p/10900334.html. If there is any infringement, please inform me in time.

The CSDN address is: https://blog.csdn.net/qq_42679573/article/details/106103729

New student blogger, dedicated to signal analysis. If you find it useful, please give it a follow~
