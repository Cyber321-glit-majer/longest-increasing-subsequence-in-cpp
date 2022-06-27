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


```
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

```
**BY USING BINARY SEARCH**
```
#include<bits/stdc++.h>
using namespace std;
class Solution
{
    public:
    //binary search function finds the position of the first integer
    //in arr[] which is greater than or equal to 'value'.
    int binarySearch(int arr[], int l, int h, int value)
    {
        //if new value is greater than all array values,
        //then it is placed at the end.
        if(value>arr[h]) 
        return h+1;
       
        //binary search algorithm.
        while(h>l)
        {
            int middle = (h+l)/2;
            
            if(arr[middle] == value)
            return middle;
            
            if(arr[middle] > value)
            h = middle;
            
            else 
            l = middle + 1;
        }
        
        return h;
    }
    
    //Function to find length of longest increasing subsequence.
    int longestSubsequence(int n, int a[])
    {
        //tail[i] holds the last value in a subsequence of length i+1.
        int tail[n];
        tail[0] = a[0];
        
         //the position of last filled index in tail[].
        int lastIndex = 0;
        
        for(int i=1; i<n; i++)
        {
            //getting the furthest possible index for a[i].
            int index = binarySearch( tail, 0, lastIndex, a[i] );
            
            tail[index] = a[i];
            //updating lastIndex.
            lastIndex = max( lastIndex, index );
        }
        //returning the result.
        return lastIndex + 1;
    }
};
int main()
{
    int n;
    cin>>n;
    int a[n];
    for(int i=0;i<n;i++)
    {
        cin>>a[i];
    }
    
    Solution sb;
    cout<<sb.longestSubsequence(n,a);
    
}

```
**DYNAMIC PROGRAMMING**

```

#include<bits/stdc++.h>
using namespace std;
class Solution {
public:
    int dp[2515];
    int lis(int i,vector<int>&a)
    {
      
        if(dp[i]!=-1)
            return dp[i];
             int ans=1; 
            for(int j=0;j<i;++j)
        {
            if(a[i]>a[j])
            {
                ans=max(ans,lis(j,a)+1);
                
            }
        }
        return dp[i]=ans;
    }
    int lengthOfLIS(vector<int>& nums) {
       memset(dp,-1,sizeof(dp));
        int ans=0;
        for(int i=0;i<nums.size();i++)
        {
           ans=max(ans,lis(i,nums));
        }
        return ans;
    }
};
int main()
{
    int n;
    cin>>n;
    vector<int>v(n);
    for(int i=0;i<n;i++)
    {
        cin>>v[i];
    }
    Solution sb;
    cout<<sb.lengthOfLIS(v);
}
