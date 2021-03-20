# Large Scale Data Processing: Project 1
# Aidan Shea
# Results
## Running the program on my local computer
| k = amount of leading zeros          | xS                                            | Hash Value                                                       | Time Elapsed  | Number of Trials  |
| :----------------------------------: | :-------------------------------------------: | :--------------------------------------------------------------: | :-----------: | :---------------: |
| 2                                    | 941271913this_is_a_bitcoin_block_of_36069131  | 00eb4fe50c034351e7880796ed9f5b645c29f9bbf547d8821b939a94f777e543 | 2s            | 100               |  
| 3                                    | 1772394281this_is_a_bitcoin_block_of_36069131 | 0009016512b19eb0f47f51d711833dfdb5cb8f6d6da5611cee62d08f0d89ec63 | 2s            | 1000              |
| 4                                    | 1127580362this_is_a_bitcoin_block_of_36069131 | 0000557effc3c441567c23018f80ee05f9da054e2e56a1ef94be2af4b79308f2 | 2s            | 50000             |
| 5                                    | 677727831this_is_a_bitcoin_block_of_36069131  | 00000fff13501523d2df83e5990a9a620a73221a90b260384b101336154c78e2 | 4s            | 500000            |
| 6                                    | 617290535this_is_a_bitcoin_block_of_36069131  | 000000934d6e17cb0bfd5451d8ccc1251919a129f9aa9c52904bd43cfa072bf8 | 5s            | 1000000           |
## Running the program on GCP
| k = amount of leading zeros          | xS                                            | Hash Value                                                       | Time Elapsed  | Number of Trials  |
| :----------------------------------: | :-------------------------------------------: | :--------------------------------------------------------------: | :-----------: | :---------------: |
| 7                                    | 44985403this_is_a_bitcoin_block_of_36069131   | 0000000936023c0b24c6bb843daf446508ea0349c545cdda31d54ae12854ab33 | 3610s         | 1000000000        |  
## Nonce Generation
### Originally the program generates the potential nonce randomly
###### val nonce = sc.range(0, trials).mapPartitionsWithIndex((indx, iter) => {
######       val rand = new scala.util.Random(indx + seed)
######       iter.map(x => rand.nextInt(Int.MaxValue - 1) + 1)
######     })
### After this modification in the code the program generates the potential nonce from 1 to n (the number of trials)
###### val nonce = sc.range(0, trials).mapPartitionsWithIndex((indx, iter) => {
######      val rand = new scala.util.Random(indx + seed)
######      iter.map(x => rand.nextInt(trials) + 1)
######     })
## Running the program on my local computer with the modified nonce code
| k = amount of leading zeros          | xS                                            | Hash Value                                                       | Time Elapsed  | Number of Trials  |
| :----------------------------------: | :-------------------------------------------: | :--------------------------------------------------------------: | :-----------: | :---------------: |
| 2                                    | 1085485955this_is_a_bitcoin_block_of_36069131 | 000f8629ddf4892605429663101a03e5e399c3ef75d119eb469018da2e063d3c | 2s            | 500               |  
| 3                                    | 1172048597this_is_a_bitcoin_block_of_36069131 | 000483edb68cb5b0dfc94cda67745f31403c32b461fe6c23a2dbc79b8244ac2e | 2s            | 5000              |
| 4                                    | 2135375646this_is_a_bitcoin_block_of_36069131 | 0000aa75a902be99b1141ba91782a4d1a78d9f8ebc6212cd7f01a267f9aa5b72 | 2s            | 75000             |
| 5                                    | 903778484this_is_a_bitcoin_block_of_36069131  | 000008e81e5ab3a018c74e8eab7eadad33bf43cb9c57024a123d19cd1b95707e | 9s            | 1000000           |
| 6                                    | 1644409016this_is_a_bitcoin_block_of_36069131 | 0000002353b6b1505f2719af10ef82c33e0a8a21d627a2ea892383dcfa91d743 | 46s           | 25000000          |
### From the data, it seems that randomly generating the nonce was more efficeint as for a given k, the program elapsed less time and required a fewer amount of trials in order to return a desired hash value.
