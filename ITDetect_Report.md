# ITDetect
## ITDetect Example
### ITDetect Command
```bash
java -jar $ITDetect/bin/ITDetect.jar \
	-b $BAMDIR/"YOUR.BAM"\
    -o $OUTDIR/"YOUR.RAW.vcf"\
    -r $ReferenceDIR/'hg19_1-22-X-Y-M.fa' \
    -t $ITDetect/data/FLT3.gene.hg19.txt #Set your target region
python $ITDetect/bin/ITDetect_Addon.py $OUTDIR/"YOUR.RAW.vcf"
```
```bash
	New Command
```

### ITDetect Result
> We designed and developed the FLT3-ITD ITDetect, which is capable of sensitive detection and provides clinical information. The following is an example of the method used to verify the performance of ITDetect and the summary of the results output by ITDetect.
> The algorithm of ITDetect and how it works are shown in the figure below.
> 
![ITDetect_Algorithm](https://user-images.githubusercontent.com/46435198/84986972-606b6980-b17a-11ea-9d09-bd2cdc1c7ef0.PNG)

> An indexed bam file is required as an input file. ITDetect outputs a text file containing the finalized information. To verify the result, we observed IGV capture that the soft-clipped read was aligned in the region, and verified the detection performance of ITDetect through comparison with other NGS-based tools.
> 
> ![ITDetect_Feature](https://user-images.githubusercontent.com/46435198/84987025-7842ed80-b17a-11ea-8e94-aaea605efed8.PNG)
> 
> Three cases are considered to be important for ITD detection, as shown in figure 3. The first case is when various sizes of ITD exist. As in the case of P01, the detection results from IGV and ITDetect were able to identify two ITDs with different sizes. NGS-based tools except ITDetect detected only one type of ITD. The second case is when the insertion is inserted between ITDs. ITD in P03 sample was detected only in 3 out of 4 NGS-based tools. The third case is when the ITD has a small Alt read count. In the case of P07 in Figure 3, For ITD in the P07 sample observed in IGV Capture, only ITDetect among NGS-based tools has detected the ITD.


