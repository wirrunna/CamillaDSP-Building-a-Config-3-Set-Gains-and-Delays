# CamillaDSP-Building-a-Config-3-Set-Gains-and-Delays
3. Measure response, determine and set set gains and delays for each driver

### Gains
This measurement shows a Full System 20-20,000Hz SPL and lets us determine the gains needed. I will leave Hi as is, drop Bass and lift Mid

![alt text](<Images/Dec 5 5 T31 81db Fs 20-20kHz Biquads and XOs.jpg>)

If we leave the Hi alone, we need to raise the mid by 3.3db and lower bass by 5.8db. So in CamillaDSP we add a Gain filter of +3.3db to the Mid pipeline and a Gain Filter of -5.8db to the Bass Pipeline.

This plot shows 3 sweeps, Bass - Orange, Mid - Green, Hi - Blue overlaid on a FS 20-20kHz sweep (Brown) before gains are adjusted and a second Full System 20-20kHz (Teal) with gains. Note the dip between 3k and 4kHz caused by out of phase drivers.

![alt text](<Images/Dec 5 6 T31 84db Gains Biquads XOs.jpg>)


### Phase
The SPL and Spectrogram plots show stuff happening at 3600Hz which is the XO frequency between Mid and Hi, the big dip at 3600Hz is classic indicator of out of phase drivers with the responses subtracting from each other, so we add an Invert Phase filter to the Hi pipeline.

### Delay
Here is a REW GD plot showing the Mid & High on 0ms and Bass arriving 5ms later
![alt text](<Images/Dec 5 5 T31 81db Fs 20-20kHz Biquads and XOs Group Delay.jpg>)

and a REW spectrogram showing the same delay
![alt text](<Images/Dec 5 5 T31 81db Fs 20-20kHz Biquads and XOs Spectrogram.jpg>)

So we add a delay filter of 5ms to the Mid and Hi pipelines.

The Impulse step response is shown for interest.
![alt text](<Images/Dec 5 5 T31 81db Fs 20-20kHz Biquads and XOs Impulse.jpg>)

Gain filters and an Invert Phase filter. I could have included the Invert Phase in one of the Gain filters but for clarity of the pipeline I leave it seperate.

![alt text](<Images/CamillaDSP gui showing Gain filters.jpg>)

With Gain and delay filters and an Invert Phase between Mid and Hi here is a Full System sweep.

![alt text](<Images/Dec 5 8 T31 84db Gains Biquads XOs 5ms delay for Mid and Hi Hi.jpg>)

This shows that once the drivers are Time Aligned the Bass and Mid are out of phase, so I just added an Invert Phase filter in the Mid pipeline.

![alt text](<Images/Dec 5 9 T31 84db Gains Biquads XOs 5ms delay and Inv Phase for Mid and Hi.jpg>)


I was surprised at exactly 5ms delay being required so I ran two more sweeps, one with delay at 4.9ms and one with delay at 5.1ms - these confirmed that the delay needed to be 5.0ms.

Here is the Pipeline with the filters added
 
![alt text](<Images/UL5 T31 Pipeline.jpg>)


### Further refining crossovers.
At this stage we have the three drivers EQualized, Time Aligned by the addition of Delays and Levels of each driver matched by applying Gains. and the first attempt of XOs done. Here are overlaid measurements of each driver showing the "raw" response, the EQ'd response and the EQ'd response with XO applied.
 


K-Horn bass does not normally go down to 30Hz, but my room is 10.8 m long (about the length of a 32Hz sound wave) so a bit of EQ will give me 30Hz with a few db loss of sensitivity which is easily compensated for in a tri-amped system with no passive crossovers. 

   The equalised mid shows a useable response of -3db at 328Hz with a steep fall below that, the so called "acoustic crossover". Trying XOs from 275Hz on up at 5Hz increments showed that a rePhase generated Hi Pass at 290Hz LR shape with a slope of 96db/octave tidied up the fall off tail and made sure that no deep bass was ever fed to the mid driver while leaving the rest of the rising frequency response alone. 

Sweeps were then taken of 20-5000 with bass XO varying from 310Hz up to 340Hz at 10Hz increments to find the frequency that summed with the mid for the flattest crossover, settling on 330Hz Low Pass with LR shape and a slope of 96db/octave.

The Mid to Hi XO was picked at 3,600Hz and sweeps taken with the Mid Low Pass eventually being moved to 3,800Hz and the Hi High Pass set at 3,600Hz, both LR shape and 48db/octave to provide the flatest response.
 
Next stage is to flatten the excess phase -

https://github.com/wirrunna/CamillaDSP-Building-a-Config-4-Get-Excess-Phase-to-Zero

