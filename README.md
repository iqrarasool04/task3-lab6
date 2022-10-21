# task3-lab6
this is task3 of lab 6 of dsa
#include <iostream>
#include <algorithm>
#include <vector>
#include <cassert>

using namespace std;

bool moveMin(vector<int>& in) {
	int temp=0;
	for (int j = in.size()-1; j > 0;j--) {
		if (in[j]<in[j-1]) {
			temp = in[j];
			in[j] = in[j-1];
			in[j-1] = temp;
				
		}
	}	
	return temp;
}

bool testMovMin(){
	//size of array
	int n = 1 + (rand() % 100);
	
	//vector input from user
	vector<int> v;
	srand(time(0));
	cout << "Array with random numbers:" << endl;
	for (int i = 0; i < n; i++) {
		int val = 1 + (rand() % 100);
		v.push_back(val);
		cout << v[i] << endl;
	}

	//random number generation
	int x = 1 + (rand()%100);

	//pushing random number in vector
	v.push_back(x);
	cout << x << endl;

	//sorting using sort function
	sort(v.begin(), v.end());
	cout << "Vector after sorting by sort: " << endl;
	for (int i = 0; i < v.size(); i++) {
		cout << v[i] << endl;
	}

	//copy test vector
	vector<int> u;
	copy(v.begin(), v.end(),back_inserter(u));

	//sort using above function
	moveMin(u);

	//printing copy vector
	cout << "Vector after sorting by moveMin: " << endl;
	for (int i = 0; i < u.size();i++) {
		cout << u[i] << endl;
	}

	//comparing vectors
	assert(u == v);
	return 0;
}

int main() {
	vector<int> v1;
	v1 = { 3,5,12,24,25,27,15 };
	moveMin(v1);
	cout << v1[3] << endl;
	cout<<testMovMin();
}
