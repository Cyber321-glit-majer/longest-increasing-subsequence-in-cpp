# longest-increasing-subsequence-in-cpp

**PROBLEM STATEMENT**

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

 

Example 1:

Input: nums = [10,9,2,5,3,7,101,18]

Output: 4

Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

Example 2:

Input: nums = [0,1,0,3,2,3]

Output: 4

**CODE**
**NORMAL APPROACH**
```
#include <bits/stdc++.h>
const int N=1e5+10;
using namespace std;
int a[N];
int solve(int i)
{int ans=1;
    for(int j=0;j<i;j++)
    {
        if(a[i]>a[j])
        {
            ans=max(ans,solve(j)+1);
        }
    }
    return ans;
}
int main()
{
    int n;
     cin>>n;
     int ans=0;
      for(int i=0;i<n;i++)
      {
          cin>>a[i];
      }
       for(int i=0;i<n;i++)
      {
          ans=max(ans,solve(i));
      }
      cout<<ans;
     

    return 0;
}

**BY USING DYNAMIC PROGRAMMING**

```
#include <bits/stdc++.h>
const int N=1e5+10;
using namespace std;
int dp[N];
int a[N];
int solve(int i)

{
    if(dp[i]!=-1)
    return dp[i];
    int ans=1;
    for(int j=0;j<i;j++)
    {
        if(a[i]>a[j])
        {
            ans=max(ans,solve(j)+1);
        }
    }
    return dp[i]=ans;
}
int main()
{
    memset(dp,-1,sizeof(dp));
    int n;
     cin>>n;
     int ans=0;
      for(int i=0;i<n;i++)
      {
          cin>>a[i];
      }
       for(int i=0;i<n;i++)
      {
          ans=max(ans,solve(i));
      }
      cout<<ans;
     

    return 0;
}
