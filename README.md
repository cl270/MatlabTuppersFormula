# Tuppers Formula in Matlab

*Part 1 of a reupload to github of pieces of my former and now defunct personal website paulsblog.us. With minor edits and updates*

## Introduction

In 2001, Jeff Tupper at the University of Toronto published a paper named Reliable Two-Dimensional Graphing Methods for Mathematical Formulae with Two Free Variables and presented it at SIGGRAPH 2001. It introduces an equation that when graphed, produces every single possible 17×106 resolution bitmap every 17 pixels on the y axis up to somewhere in the range of 17·1802! (That’s 1802 Factorial – every number from 1 to 1802 multiplied by each other: 1·2·3·4·5…·1801·1802), which is the total number of possible images in a 17×106 resolution bitmap, considering only black and white. This set of bitmaps includes literally every bitmap possible in a 17x106 resolution, including an upside-down pixellated version of itself (hence why it was termed Tupper’s Self Referential Formula) between the value k =

960 939 379 918 958 884 971 672 962 127 852 754 715 004 339 660 129 306 651 505 519 271 702 802 395 266 424 689 642 842 174 350 718 121 267 153 782 770 623 355 993 237 280 874 144 307 891 325 963 941 337 723 487 857 735 749 823 926 629 715 517 173 716 995 165 232 890 538 221 612 403 238 855 866 184 013 235 585 136 048 828 693 337 902 491 454 229 288 667 081 096 184 496 091 705 183 454 067 827 731 551 705 405 381 627 380 967 602 565 625 016 981 482 083 418 783 163 849 115 590 225 610 003 652 351 370 343 874 461 848 378 737 238 198 224 849 863 465 033 159 410 054 974 700 593 138 339 226 497 249 461 751 545 728 366 702 369 745 461 014 655 997 933 798 537 483 143 786 841 806 593 422 227 898 388 722 980 000 748 404 719

and k + 17.

It also includes a right side up version between k =

4858450636189713423582095962494202044581400587983244549483093085061934704708809928450644769865524364849997247024915119110411605739177407
8569197543265718554420572104457358836818298237541396343382251994521916512843483329051311931999535024137587652392648746133949068701305622
9581321948111368533953556529085002387509285689269455597428154638651073004910672305893358605254409666435126534936364395712556569593681518
4334857605266940161251266951421550539554519153785457525756590740540157929001765967965480064427829131488548259914721248506352686630476300

and k + 17.

## Formula

Tupper’s Self Referential Formula can be written as 1/2 < mod(⌊ ⌊ y/17 ⌋ · 2^{-17·⌊ x ⌋ - mod(⌊ y ⌋, 17)}, 2 ⌋),

## Rationale

I’ve decided to use Matlab for this project, due to Matlab having built in plotting subroutines that make data visualization much easier to code.

In the code, I customarily clear all of the previously stored data and forms with a clear all, close all. The constant k represents a symbolic value (since declaring k as a regular variable would cause a massive overflow error for even 64 bit data types) that splits the value k above into chunks that are stitched together.

I then declare a 2D meshgrid (just Matlab’s way of preparing a rectangular grid) of dimensions 17×107, tell it to calculate the formula with the value of k given to it, and since k was declared as a symbolic number, I convert it back to the more commonly used 64-bit double to prevent any incompatibility later on.

As I mentioned earlier, the formula produces an inverted version of itself with this value of k, so I flip the bitmap array produced by the formula from left to right. The rest of the code deals with the graphing of the data. Changing the color scheme to gray, equalizing the axes, labeling the graph etc.

## Modifying "k" for a custom bitmap

By changing “k” you’re able to move up and down the graphs that Tupper’s formula draws. To create your own images with the code I posted, and for a deeper understanding of how the formula works, think of the following:

k is always a multiple of 17 since the bitmap has a height of 17 pixels.
For a bitmap containing the first black pixel in the bottom right k=17*1=17. Binary conversion of the decimal 1 is 1.
Tupper's Formula when k=17

For a bitmap containing the second pixel (first is white) from the bottom right k = 17*2 = 34. Binary conversion of the decimal 2 is 10.
For a bitmap containing both the second pixel and first pixel from the bottom right k = 17*3 = 51. Binary conversion of the decimal 3 is 11.
For a bitmap containing only the third pixel (second and first are white) from the bottom right k = 17*4 = 68. Binary conversion of the decimal 4 is 100.
So we’re seeing a pattern here: the multiplier of 17 when, converted to binary, determines which pixels are colored. Let’s test that theory. Let’s color the 7th, 5th, and 1st pixels. That should be 1010001 in binary right? 1010001 in binary/base two is 81 in decimal/base ten. 81*17 = 1377. So let’s try k = 1377:
Tupper's Formula when k=1377

Success! So by iterating along each of the pixels down to up and right to left in binary (1 if dark, 0 if not), converting that binary number to decimal and multiplying by 17, you can create your own “k’s” to draw your own pictures.

## Fun Bitmaps

Using this method, I was able to find my initials PL between by changing the definition of k in the code to k =

9737153153655710815027092553582736311139079827536572503883519993232732261745884141124799337662417491264

3380373975764218156909277833829923765820783492836069108194758552159846628078012260081526540816377495

7100070214261575315224270033921774452265835298816

and k+17:

Tupper's Formula drawing the letters P L

And the Galaga ship between k =

162929142561716796442986023622873541917068577381867468424885514871843876614316586042575907568

73665084346200859900217385528810674732019298903742312228519601135004225221550931968

and k + 17

Tupper's Formula Drawing the Galaga Ship

## Conclusion

Credits to Numberphile on Youtube for informing me on the formula. I highly recommend it!

As an aside, the existence of a massive number of possible outcomes is similar to the numberspace of possible private keys in crytosecurity systems with a sufficiently high key size, like in some cryptocurrencies like Bitcoin and Ethereum. keys.lol is a good site to browse through the huge 2^160 possible private/public key combinations of both cryptocurrencies.
