# CamillaDSP-Building-a-Config-3-Set-Gains-and-Delays
3. Measure response, determine and set set gains and delays for each driver

### Gains
This measurement shows a Full System 20-20,000Hz SPL and lets us determine the gains needed.
![alt text](<Images/REW V5.40 FS EQs XO.jpg>)
REW V5.40 FS EQs XO.jpg

If we leave the Bass alone, we need to raise the Mid by 4.35db and Hi by 6.5db. So in CamillaDSP we add a Gain filter of +4.35db to the Mid pipeline and a Gain filter of 6.5db to the Hi Pipeline.

This plot shows the first attempt at gains and then with the gains reduced a further 0.8db.
![alt text](<Images/REW V5.40 FS adjust gains.jpg>)
REW V5.40 FS adjust gains.jpg


### Delay
Here is a REW GD plot showing the Mid & High on 0ms and Bass arriving 5ms later
![alt text](<Images/REW V5.40 FS EQ XO Gains IPh - GD.jpg>)
REW V5.40 FS EQ XO Gains IPh - GD.jpg

and a REW spectrogram showing the same delay
![alt text](<Images/REW V5.40 FS EQ XO Gains IPh - Spectrogram.jpg>)
REW V5.40 FS EQ XO Gains IPh - Spectrogram.jpg


So we add a delay filter of 5ms to the Mid and Hi pipelines. I could include the Invert Phase in one of the Gain filters but for clarity of the pipeline I leave it seperate.
![alt text](<Images/CamillaDSP Gui Pipeline tab showing Invert Phase Gains and Delay filters.jpg>)
CamillaDSP Gui Pipeline tab showing Invert Phase Gains and Delay filters.jpg

With Gain and delay filters and an Invert Phase between Mid and Hi here is a Full System sweep.

![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm.jpg 

GD plot
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm - GD.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm - GD.jpg

Step Response
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm - Step Response.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm - Step Response.jpg

Spectrogram
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm - Spectrogram.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm - Spectrogram.jpg


I was surprised at exactly 5ms delay being required so I ran two more sweeps, one with delay at 4.9ms and one with delay at 5.1ms - these confirmed that the delay needed to be 5.0ms.

Here is the Pipeline with the filters added
![alt text](<Images/CamillaDSP GUI Pipeline tab pipeline plot EQs XO Gain Delay InvPh.jpg>) 
CamillaDSP GUI Pipeline tab pipeline plot EQs XO Gain Delay InvPh.jpg


### Further refining crossovers.
At this stage we have the three drivers EQualized, Time Aligned by the addition of Delays and Levels of each driver matched by applying Gains and the first attempt of XOs done.

K-Horn bass does not normally go down to 30Hz, but my room is 10.8 m long (about the length of a 32Hz sound wave) so a bit of EQ will give me 30Hz with a few db loss of sensitivity which is easily compensated for in a tri-amped system with no passive crossovers. 

The equalised mid shows a useable response of -3db at 328Hz with a steep fall below that, the so called "acoustic crossover". Trying XOs from 275Hz on up at 5Hz increments showed that a rePhase generated Hi Pass at 290Hz LR shape with a slope of 96db/octave tidied up the fall off tail and made sure that no deep bass was ever fed to the mid driver while leaving the rest of the rising frequency response alone. 

Sweeps were then taken of 20-5000 with bass XO varying from 310Hz up to 340Hz at 10Hz increments to find the frequency that summed with the mid for the flattest crossover, settling on 330Hz Low Pass with LR shape and a slope of 96db/octave.

The Mid to Hi XO was picked at 3,600Hz and sweeps taken with the Mid Low Pass eventually being moved to 3,800Hz and the Hi High Pass set at 3,600Hz, both LR shape and 96db/octave to provide the flatest response.
 
Next stage is to flatten the excess phase -

https://github.com/wirrunna/CamillaDSP-Building-a-Config-4-Get-Excess-Phase-to-Zero

