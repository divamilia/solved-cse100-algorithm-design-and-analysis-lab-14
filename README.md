Download Link: https://assignmentchef.com/product/solved-cse100-algorithm-design-and-analysis-lab-14
<br>
<h1>Huffman Codes</h1>

Suppose that we have to store a sequence of symbols (a file) efficiently, namely we want to minimize the amount of memory needed. For the sake of simplicity we assume that the symbols are restricted to the first 6 letters of the alphabet. For example, let us assume that the frequency of different symbols that you have to store are the following:

<h2>                                                                                       symbol   frequency</h2>

A    1000 B            150 C       200 D  800 E  300

<h2>F          50 Total          2500</h2>

As we have to store 6 different symbols, the obvious way is to encode each of them in 3 bits, as with 3 bits it is possible to encode 2<sup>3 </sup>different symbols. With this encoding, we need 2500×3 = 7500 bits to store the above symbols.

A different strategy to address the problem is the following. Instead of assigning to each symbol a code with the same length (i.e., number of bits), we assign shorter codes to symbols that are more frequent, and longer codes to symbols that are less frequent. One possible encoding according to this sequence is the following:

<h2>symbol            encoding A     0 B       10101 C          1011 D            11 E     100 F  10100</h2>

According to this encoding the number of required bits is:

<h2>1000 × 1 + 150 × 5 + 200 × 4 + 800 × 2 + 300 × 3 + 50 × 5 = 5300</h2>

This idea is at the basis of the programs used to compress files. First, they analyze the input, then they choose the codes, and then they recode the input according to the determined codes.

While this idea brings benefits in terms of the space requirements, using variable length codes presents some problems. Once we have coded a file according to a variable length code, we must also be able to decode it in the original format (i.e., once we have compressed the file, we want to be able to decompress it). The encoding works only if the codes assigned to different characters are such that no code is a prefix of any other code. If this property does not hold, there is a problem of ambiguity when trying to decompress the sequence.

You can prove that in the depicted example no code is a prefix of any other code. For example: no code starts with 0 except for the code of <em>A</em>. So, while decompressing the file, if we find a

symbol whose code starts with 0, we know it is <em>A</em>. If we find a character whose code starts with 11, we know it is <em>D</em>. It cannot be any other symbol, as no code starts with 11 other than <em>D</em>. And so on. How do we assign codes? This is done through a greedy algorithm. We assign the shortest code to the most frequent character, the second longest one to the second most frequent character, and so on. The figure below illustrates the first few stages of the algorithm.

<table width="455">

 <tbody>

  <tr>

   <td width="63">A: 1000</td>

   <td width="16"> </td>

   <td width="63">B: 150</td>

   <td width="16"> </td>

   <td width="63">C: 200</td>

   <td width="16"> </td>

   <td width="63">D: 800</td>

   <td width="16"> </td>

   <td width="63">E: 300</td>

   <td width="16"> </td>

   <td width="63">F: 50</td>

  </tr>

 </tbody>

</table>

1)

Given <em>N </em>characters with their respective frequencies, the algorithm initially builds <em>N </em>trees, each one consisting just of a single node (step 1, in the figure). Then, iteratively, it joins together the trees whose roots have the lowest frequencies (steps 2, 3, etc. in the figure). The tree with the lowest root frequency becomes the left child and the tree with the second-lowest root frequency becomes the right child. Left children are associated with the bit 0, right children with the bit 1. Internal nodes (i.e., root nodes created) can be thought of as dummy nodes storing a fictitious character (which does not appear in our sequence). This procedure is iterated until there is just one tree. At this point, in order to know the code associated with one symbol you simply need to concatenate the 0s and 1s you encounter while moving from the root down to the symbol.

Note that the greedy strategy is applied in the reverse way. Symbols with low frequencies end up down in the tree (i.e., they are associated with long codes), while nodes with high frequencies are near the root (i.e., they are assigned short codes).

<strong>Input structure </strong>On the first line in the input is the number of characters <em>N </em>in the alphabet.

Each of the following <em>N </em>lines contains the frequency of the <em>i</em><sup>th </sup>symbol, one per line.

<strong>Output structure </strong>The output contains <em>N </em>lines. Each line prints the Huffman code corresponding to the <em>i</em><sup>th </sup>symbol in the input.