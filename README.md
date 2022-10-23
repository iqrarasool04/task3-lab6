# task3-lab6
this is task3 of lab 6 of dsa
#include <iostream>
#include <algorithm>
#include <vector>
#include <cassert>
#include <chrono>

using namespace std;
using namespace std::chrono;

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
	int n = 1 + (rand() % 100000);
	
	//vector input from user
	vector<int> v;
	srand(time(0));
	cout << "Vector with random numbers:" << endl;
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

	//start time
	auto start = high_resolution_clock::now();

	//sorting using sort function
	sort(v.begin(), v.end());
	cout << "Vector after sorting by sort: " << endl;
	for (int i = 0; i < v.size(); i++) {
		cout << v[i] << endl;
	}
	//stop time
	auto stop = high_resolution_clock::now();

	//time calculation used by sort function
	auto duration = duration_cast<microseconds> (stop - start);
	cout << "Time taken by sort function: " << duration.count() << " microseconds" << endl;

	//copy test vector
	vector<int> u;
	copy(v.begin(), v.end(),back_inserter(u));

	//start time
	auto start1 = high_resolution_clock::now();

	//sort using above function
	moveMin(u);

	//printing copy vector
	cout << "Vector after sorting by moveMin: " << endl;
	for (int i = 0; i < u.size();i++) {
		cout << u[i] << endl;
	}
	//stop time
	auto stop1 = high_resolution_clock::now();

	//time calculation used by sort function
	auto duration1 = duration_cast<microseconds> (stop1 - start1);
	cout << "Time taken by moveMin function: " << duration1.count() << " microseconds" << endl;

	int best_case;
	int worst_case;
	int average_case = duration1.count();
	for (int i = 0; i < 100; i++) {
		//if (i == 0) {
		best_case = 0;
		worst_case = 0;
		//}
		if (duration1.count()<best_case) {
			best_case = duration1.count();
		}
		else if (duration1.count() > worst_case) {
			worst_case = duration1.count();
		}
		
		average_case = average_case / 100;
	}
	cout << "Best case running time is: " << best_case << endl;
	cout << "Worst case running time is: " << worst_case << endl;
	cout << "Average case running time is: " << average_case << endl;

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
