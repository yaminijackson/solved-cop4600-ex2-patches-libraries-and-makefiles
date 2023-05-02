Download Link: https://assignmentchef.com/product/solved-cop4600-ex2-patches-libraries-and-makefiles
<br>



<h1>Overview</h1>

In this exercise you will learn about patches, libraries and Makefiles. You will first modify the patch you created for Project 0. You will then create a static library that will perform a simple arithmetic operation and finally you will create a Makefile to compile that library.

<h1>Structure</h1>

The project is broken into three main parts:




<ul>

 <li>Modify the patch file from P0.</li>

 <li>Create a static library.</li>

 <li>Create a Makefile to re-compile your library.</li>

</ul>




<h2>Patch Files<a href="#_ftn1" name="_ftnref1"><sup><strong>[1]</strong></sup></a></h2>

A patch file is a text file that contains instructions on how to update other files. In Project 0 you modified a certain file(s) to add your name to the boot message. You then rebuilt the kernel and saw that your changes were applied successfully (hopefully)! Finally, you created a patch that contained all the changes. In other words, the patch contained the <em>differences</em> between your modified source and the original clean source you downloaded. Here’s an example patch file:




The first 5 lines specify which file to modify. The remainder indicates which lines are removed and inserted. When applying this patch file to a clean source of your file system, the patch program will know exactly what to remove and what to add.




Patches are useful because they only keep track of changes. (Imagine if you had to export the

1.4 GB Reptilian image and upload it to Canvas every time you had to submit something!)




For this exercise you will need to do the following:




<ol>

 <li>Create a patch file to remove the message you added in P0 and insert a new one that prints “<strong><em>### First Last Name (Exercise 2) ###</em></strong>” by modifying your P0 patch.</li>

</ol>




<strong><em>NOTE</em></strong>: You will apply the patch to the kernel source that already contains the changes from P0, so you will need to remove the P0 changes and add the new changes.




<ol start="2">

 <li>You will apply the patch by switching to <strong>/usr/rep/src/reptilian-kernel</strong> and running:</li>

</ol>




<strong>$</strong><strong> git apply patch_name.diff  </strong><strong>$</strong><strong> make &amp;&amp; sudo make install &amp;&amp; sudo make modules_install </strong>




<ol start="3">

 <li>Take a <u>screenshot of the boot message showing the modified message</u>.</li>

</ol>







<h2>Libraries<a href="#_ftn2" name="_ftnref2"><sup><strong>[2]</strong></sup></a></h2>

Libraries are simply a collection of previously defined declarations and procedures. If we often use the same subroutines, we can create a library and use it across all our projects. For example, we can use a math library to perform matrix multiplication. You can read about different types of libraries here: <a href="http://www.hep.wisc.edu/~pinghc/generate_your_own_library.htm">http://www.hep.wisc.edu/~pinghc/generate_your_own_library.htm</a>




In this project you will create a simple static library using the following steps:




<ol>

 <li>Create <strong>c</strong> in <strong>/home/reptilian/math</strong>. (You will need to create the <strong>math</strong> directory.)</li>

</ol>

<strong> int mean(int a, int b) </strong>

<strong>{ </strong>

<strong> return (a + b) / 2; </strong>

<strong>} </strong>




<ol start="2">

 <li>Create the <strong>h</strong> in <strong>/home/reptilian/math</strong>.</li>

</ol>

<strong> </strong>

<strong>#pragma once </strong>

<strong>int mean(int a, int b); </strong>

<em> </em>

<ol start="3">

 <li>Compile <strong>c</strong> and create <strong>libmath.a</strong>.</li>

</ol>




<h3>$ cc -c mean.c  $ ar cr libmath.a mean.o</h3>

<ol start="4">

 <li>Create <strong>c</strong> in <strong>/home/reptilian</strong>.</li>

</ol>

<strong> </strong>

<strong>#include &lt;stdio.h&gt; </strong>

<strong>#include “math/mean.h” </strong>

<strong> int main() { </strong>

<strong> printf(“The average between 3 and 5 is %d
”, mean(3, 5));  return 0; </strong>

<strong>} </strong>




<ol start="5">

 <li>Compile and run <strong>c</strong>.</li>

</ol>




<strong>$ </strong><strong>cc</strong> <strong>-o test test.c -L ./math -lmath </strong> <strong>$ </strong><strong>./test</strong>




<ol start="6">

 <li>Take a <u>screenshot of the output.</u></li>

</ol>







<h2>Makefiles</h2>

Makefiles are used to organize code compilation. Earlier in this exercise you manually entered the commands to create your library… but imagine if you had to compile this and 50 other programs! In such a circumstance, <strong>Makefiles</strong> come in handy. A Makefile contains all the instructions needed to compile programs and can be run with the <strong>make</strong> command. For this exercise you will create a Makefile in <strong>/home/reptilian/math</strong> that will compile the library.




Read about Makefile here: <a href="http://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/">http://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/</a>




To test it and make sure it works, delete <strong>libmath.a</strong> and <strong>mean.o</strong>, then run <strong>make. </strong>This should re-create <strong>libmath.a</strong> and <strong>mean.o</strong>. Submit <u>t</u>he <u>Makefile</u> on Canvas. (You can add the “.txt” extension if necessary.)

<a href="#_ftnref1" name="_ftn1"><strong>[1]</strong></a> https://www.drupal.org/node/367392,https://en.wikipedia.org/wiki/Patch_(Unix)

<a href="#_ftnref2" name="_ftn2"><strong>[2]</strong></a> https://www.cs.swarthmore.edu/~newhall/unixhelp/howto_C_libraries.html