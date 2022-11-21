
# Matrix Problem 
### Using BFS Recursive Function
## About the Problem Statement:
Step1: Create a 10x10 matrix
<br/>
Step2: Populate the matrix with random numbers between -25 to +25
<br/>
Step3: Select two arbitrary locations from the matrix which are minimum FIVE rows
apart.
<br/>
Step4: Find the path between two locations: such that the path does not use “Diagonal”
elements. The sum of numbers present on the path between two cells should
a) Maximum
b) Minimum
<br/>
Solution is designed, with an approach to avoid using each and every element of the matrix in computation.
## Test Cases
Test case 01-
<br/>
(0,0) to (4,4)
<br/>
Output 01: <br/>
Enter initial value of x:0
<br/>
Enter initial value of y:0
<br/>
Enter final value of x:4
<br/>
Enter final value of y:4
<br/>
Maximum value: 155
<br/>
The path is as follows:
16 -> -9 -> 19 -> 7 -> 12 -> 19 -> 0 -> 8 -> 9 -> 6 -> 19 -> 10 -> -9 -> 23 -> 8 -> 5 -> 12 -> 
<br/>
Minimum value: -78
<br/>
The path is as follows:
16 -> -9 -> -22 -> -20 -> -15 -> 8 -> 0 -> -17 -> 12 -> 7 -> -19 -> -7 -> 1 -> -25 -> 12 -> 
<br/>
Test case 02-
<br/>
(0,0) to (4,1)
<br/>
Output 02: <br/>
Enter initial value of x:0
<br/>
Enter initial value of y:0
<br/>
Enter final value of x:4
<br/>
Enter final value of y:1
<br/>
Maximum value: 124
<br/>
The path is as follows:
16 -> -9 -> 19 -> 7 -> 12 -> 19 -> 0 -> 8 -> 9 -> 6 -> 19 -> 10 -> -9 -> 23 -> 8 -> 5 -> 12 -> -25 -> 1 -> -7 -> 
<br/>
Minimum value: -82
<br/>
The path is as follows:
16 -> -9 -> -22 -> -20 -> -15 -> 8 -> 0 -> -17 -> 8 -> -25 -> 1 -> -7 -> 
<br/>
## Code:
```
#include <bits/stdc++.h>
using namespace std;
int max_ans = INT_MIN;
int min_ans = INT_MAX;
vector<int> vmax;
vector<int> vmin;
const int n = 5; // For creating a 10X10 matrix
void BFS(int a[n][n], int visited[n][n], int x, int y, int sum, int fx, int fy, vector<int> v)
{
    if (x < 0 || y < 0 || x > n - 1 || y > n - 1)
    {
        return;
    }
    sum += a[x][y];
    v.push_back(a[x][y]);
    visited[x][y] = 1;
    if (x == fx && y == fy)
    {
        if (sum > max_ans)
        {
            max_ans = sum;
            vmax = v;
        }
        if (sum < min_ans)
        {
            min_ans = sum;
            vmin = v;
        }
        visited[x][y] = 0;
        return;
    }
    if (visited[x + 1][y] == 0)
    {
        BFS(a, visited, x + 1, y, sum, fx, fy, v);
    }
    else if (visited[x][y + 1] == 0)
    {
        BFS(a, visited, x, y + 1, sum, fx, fy, v);
    }
    else if (visited[x - 1][y] == 0)
    {
        BFS(a, visited, x - 1, y, sum, fx, fy, v);
    }
    else if (visited[x][y - 1] == 0)
    {
        BFS(a, visited, x, y - 1, sum, fx, fy, v);
    }
    visited[x][y] = 0;
}
int main()
{
    int x = 0, y = 0;
    int fx = 0, fy = 0;
    int a[n][n]; // A 10x10 matrix (n is a global variable)
    vector<int> v;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            int r = rand() % (25 - -25 + 1) + -25;
            a[i][j] = r;
        }
    }

    int visited[n][n]; // Initially visited matrix is initialized with 0
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            visited[i][j] = 0;
        }
    }
    // Taking input from user
    cout << "Enter initial value of x:";
    cin >> x;
    cout << "Enter initial value of y:";
    cin >> y;
    cout << "Enter final value of x:";
    cin >> fx;
    cout << "Enter final value of y:";
    cin >> fy;
    // Calling the breadth first search function
    BFS(a, visited, x, y, 0, fx, fy, v);
    cout << "Maximum value:" << max_ans << endl;
    cout << "The path is as follows:";
    for (auto m : vmax)
        cout << m << "->";
    cout << endl;
    cout << "Minumum value:" << min_ans << endl;
    cout << "The path is as follows:";
    for (auto m : vmin)
        cout << m << "->";
    return 0;
}
```
## Implementation and Procedure:
We have declared some global variables, two vector arrays which will let us store our final results  in the output.
In the main function we declared an array of size nxn (here n=10) , generating random numbers for the array 'a' using random function
Then we declared visited array of dimension nxn which is initialized to 0 that indicated no vertex has been visited yet.
After the vertex that is visited we initialize the value 1 at that position which is visited. A recursive function BFS has been called
which updates the sum accordingly where there are multiple if conditions to update the value of sum. Used backtracking algorithm 
to solve our problem statement and thus lastly printing our final result using the auto function by traversing the vmin and vmax array.
<br/>
Time Complexity: n*O(2^n) <br/> where, n= order of matrix
