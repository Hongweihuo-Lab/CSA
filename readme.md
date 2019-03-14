#Compressed-Suffix-Array(CSA)

## What is it?
	 CSA is a practical implementation of the compressed suffix arrays (CSA) theory, 
	 introduced by Roberto Grossi and Jeffrey Scott Vitter. CSA retains the high-order 
	 entropy-compressed theoretical performance and introduces some improvements in practice.
	 
	 counting: compute the number of occurrences of a pattern P in the text T.
	 locating: report the list of positions, where P occurs in T.
	 extract: extraction of arbitrary portions of text T. 
	 
## How to use it?
###just for fun
	 step 1:download or clone it
	 step 2:make
	 step 3:run my_csa
###build your own program
	 step 1:download or clone it
	 step 2:make
	 step 3:include CSA.h
	 step 4: g++ your_program.cpp -o xx -csa.a

###example
	```cpp
	#include"CSA.h"
	#include<iostream>
	using namespace std;
	int main()
	{
		CSA csa("filename");
		int num;
		csa.counting("the",num);
		cout<<"pattern the occs "<<num<<" times"<<endl;
		int *pos=csa.locating("love",num);
		cout<<"pattern love occs "<<num<<" times"<<endl;
		cout<<"all the positions are:";
		for(int i=0;i<num;i++)
			cout<<pos[i]<<endl;
		delete [] pos;//it's your duty to delete pos.
		pos=NULL;

		int start=0;
		int len =20;
		unsigned char *sequence=csa.extracting(start,len);
		cout<<"T[start...start+len-1] is "<<sequence<<endl;

		csa.save("index.csa");//serialize the fm object to file index.csa
		CSA csa2;
		csa2->load("index.csa");//restore the fm object from file index.csa

		return 0;
	}
	```
## Suffix Array Construction
The current version uses Yuta Mori's fast suffix array construction library [libdivsufsort](http://code.google.com/p/libdivsufsort/) version 2.0.1.

## Contributors
### code
•	Longgang Chen （陈龙刚）
### paper
H. Huo, L. Chen, J. S. Vitter, and Y. Nekrich, A Practical Implementation of Compressed Suffix Arrays with Applications to Self-indexing, Data Compression Conference (DCC), Snowbird, USA, 2014, 292–301. 

##ChangeLog  
2014.6.7: We can borrow hybrid-ideas in My Czip project, mix pure-gamma and rl-gamma. It would be helpful for compression.

2014.10.27: fix a bug in CSA. Decompress, about memory leak
