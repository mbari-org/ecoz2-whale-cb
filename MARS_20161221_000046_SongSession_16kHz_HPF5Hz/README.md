**Note**. In this case, the source sound file:
 
    532M ~/Downloads/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.wav
 
is located outside of this repository.
Also, the generated data is for the moment *not* included in the repo; 
only included are the resulting plots as referenced in this page. 
 
## LPC analysis

    $ lpc -P 36 ~/Downloads/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.wav
    Number of classes: 1
    class 'MARS_20161221_000046_SongSession_16kHz_HPF5Hz': 1
      /Users/carueda/Downloads/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.wav
    lpaOnSignal: P=36 numSamples=266117287 sampleRate=16000 winSize=720 offset=240 T=1108820
    data/predictors/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.prd: 'MARS_20161221_000046_SongSession_16kHz_HPF5Hz': predictor saved

## Codebook generation
    
1,108,820 training vectors.
     
    $ vq.learn -P 36 -e 0.0005 data/predictors/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.prd

Plot general evaluation:

    $ cb.plot_evaluation.py data/codebooks/_/eps_0.0005.rpt.csv

![](cb_evaluation.png)    

Cell cardinality and distortions for M=1024:
    
    $ cb.plot_cards_dists.py data/codebooks/_/eps_0.0005_M_1024.cbook.cards_dists.csv
        
![](cb_cards_dists.png)

As a scatter plot:

    $ cb.plot_cards_dists.py --scatter data/codebooks/_/eps_0.0005_M_1024.cbook.cards_dists.csv

![](cb_cards_dists_scatter.png)    

Extract  k_1 and k_2 from the training vectors:

    $ prd.show -k -r 1-2 data/predictors/MARS_20161221_000046_SongSession_16kHz_HPF5Hz/MARS_20161221_000046_SongSession_16kHz_HPF5Hz.prd > k1k2.csv
    
and from the codebooks:

    $ for M in 0002 0004 0008 0016 0032 0064 0128 0256 0512 1024; do
        cb.show -r 1-2 data/codebooks/_/eps_0.0005_M_$M.cbook > data/codebooks/_/eps_0.0005_M_$M.cbook.kk.csv
    done

With the above set of reflection coefficients, let's generate a few "k_1 vs. k_2"
scatter plots:

    $ for M in 0002 0008 0032 0128 0512; do
        cb.plot_reflections.py k1k2.csv data/codebooks/_/eps_0.0005_M_$M.cbook.kk.csv
    done

(Note: A maximum of 8000 training vectors, randomly chosen in each case, are plotted.)

M=2:
 
![](cb_kk_training_8000_codebook_2.png)

M=8:

![](cb_kk_training_8000_codebook_8.png)

M=32:

![](cb_kk_training_8000_codebook_32.png)

M=128:

![](cb_kk_training_8000_codebook_128.png)

M=512:

![](cb_kk_training_8000_codebook_512.png)

Similar reflection coefficient inspection but now with 3 coefficients:
    
    $ prd.show -k -r 1-3 data/predictors/_/HBSe_20170128T231621.prd > data/predictors/_/HBSe_20170128T231621.prd.kkk.csv
    
    $ cb.show -r 1-3 data/codebooks/_/eps_0.0005_M_1024.cbook > data/codebooks/_/eps_0.0005_M_1024.cbook.kkk.csv
    
    $ cb.plot_reflections.py kkk.csv data/codebooks/_/eps_0.0005_M_1024.cbook.kkk.csv
    df_training points = 1108820
    df_training plotted points = 8000
    df_codebook points = 1024

![](cb_kkk_training_8000_codebook_1024.png)
