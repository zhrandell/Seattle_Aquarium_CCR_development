# bull_kelp_tracking 

## Background
Monitoring kelp forests requires estimates of kelp abundance/density. 
Multiple methods of estimating kelp density exist, including drone imagery and [kayak surveys](http://mappocean.org/wp-content/uploads/2021/07/MaPP_Kelp_Monitoring_Methods_2021.pdf) of the kelp canopy (the portions of kelp that reach the sea surface, and thus are visable to aerial sensors).
Additionally, scuba divers manually count kelp stipes (with “stipes” being the vertical structure, or “tree trunk” analog of kelp), often along 30x2m underwater transects. 
These are the most precise methods, with divers counting individual stipes by hand. 

In order to extract metrics of kelp abundance from our forward-facing ROV video in an efficient manner, we attempted to implement an open-source machine learning solution. 
Specifically, we used [VIAME](https://github.com/VIAME/VIAME?tab=readme-ov-file), a AI annotation and analysis platform developed by Kitware enabling “object detection” of individually conspicuous objects (individuals) such as sea stars, sea urchins, etc. 
As a (non bull kelp) example of how our work is utilizing VIAME, see [here](https://viame.kitware.com/#/viewer/65f9a6c9481fe4ee851404f1) for example manual annotations from the downward-facing camera - a simpler use case not requiring object tracking, as the downward-facing camera generates non-overlapping still images. 

In the process of generating the manually annotated transect linked above, multiple challenges became apparent, such that in contrast to all other computer vision applications attempted thus far, we decided to pull back and seek additional guidance to identify the best approach. 
Specifically, we are uncertain if VIAME is the best open-source program, or if some other platform is more suited.
A step further, given the challenges listed below in **The Problem** section, we are uncertain if AI methods of image analysis in general are appropriate for these stipe counts, or if we ought to simply count bull kelp stipes manually via human observers reviewing the video.  

* To see a complete ROV transect from the forward-facing camera with stills extracted at 2 second interval, see [here](https://viame.kitware.com/#/viewer/6650f76027e66d3c73937562). This transect has been fully annotated manually in VIAME.

* See the DropBox folder [here](https://www.dropbox.com/scl/fo/tb4zhxbxcydjcw2ulzn2x/AI6hLC_uTVSKmR7yAzxr_oA?rlkey=r5gdlz5lt1hvicb9o6ueq0ofh&dl=0) for example still images of bull kelp stipes from the ROV.

* See [here](https://drive.google.com/file/d/1RK28xmY8yo-FMqfbQtPPxmdujq9r2AEu/view?usp=drive_link) to see the raw 4K, 30 frame per second video we shoot on our ROV. This video includes numerous instances of bull kelp. 

## The Problem 
The need to detect and track bull kelp stipes from forward-facing ROV video has several unique computer vision challenges. 

* While bull kelp stipes are visually distinctive (narrow dark “lines” arrayed vertically throughout an image), they may be a non-standard visual challenge. 

* We need to track stipes from one frame (extracted still image) to the next, i.e., object tracking. Yet there is a tradeoff - between effort and the frequency of stills we extract (see the final point in this section below). 

* At which point does the algorithm first detect the stipe? Stipes first appear in the distance, and as the ROV moves closer, become more visually resolved against their background. 

* Varying background: stipes may have the water column behind them (providing excellent contrast) or the seafloor behind them (providing much less visual contrast, as the seafloor and stipe will be similarly colored). 

* Bull kelp stipes often grow in close proximity to one another, and multiple stipes can become tangled together (in what we call a “bundle” of stipes). Bundles can consist of 2, 3, 4, or any number of bull kelp stipes. In the manually annotated kelp imagery above, we have created three "categories" of stipe: **1** `KE_stipe` - a single kelp stipe, **2** `KE_SBST` - a small bundle of stipes, i.e., two or three stipes, and **3** `KE_LBST` - a large bundle of stipes, i.e., four or more stipes. It remains unknown if these are the optimal categories, or if computer vision solutions can resolve the differences between bundles. 

* In thick forests, bull kelp stipes may also run horizontal across our ROV image, as the bull kelp gets tangled in various ways. 

* What is the appropriate still image interval? Too long of an interval (e.g., extract 1 image per 10 seconds) will result in missing stipes, whereas a very short interval (e.g., 1 image per 1 second) will prevent us from missing stipes, but may result in more laborious manual annotations - i.e., a trade-off between the completness of our annotations and mannual annotation effort.  

## The Proposed Solution
Unknown.
As field biologists, our expertise in this domain is limited. 
We are open to ideas. 

## Next Steps
A 2 second interval appears to be an appropriate frequency to track stipes abundances. 
We are prepared to provide as much forward-facing imagery as desired to test ML solutions. 

## Caveats
As this computer vision problem has proven challenging for us, we have resorted to manually reviewing our ROV videos and recording stipe and bundle counts in an excel sheet. 
It is our hope that a computer vision solution can be identified going forward. 
 

