+++
title = "LightOj 1060 (nth Permutation)"
date = "2019-05-09"
author = "~5 min read"
tags = ["lightoj", "cp", "problem solving" ,"dp" ,"combinatorics"]
description = "nth Permutation"
+++

# Idea
---
DP

- First of all we check maximum number of permutations possible from the
given string ... if it is < n than ans is impossible.
- Now we have to fix  character at each position starting from msb position 
- For fixing the character at any position initially we try to fix smallest character
at that position if by placing that character number of permutation formed >=  remaining
required permutation than fix this charter at that position ,
and decrease the frequency of this character since this character  is used at this
position and move to next position , else if no of permutation formed by placing this
character is less than the required remaining permutation than decrease remaining
permutation by the number of permutation formed by placing this character at that
position ( since  this count times number of permutations comes in between current
to final permutation ) and try to find next character for this position .

```cpp

/**Which of the favors of your Lord will you deny ?**/

#include<bits/stdc++.h>
using namespace std;

#define LL long long
#define PII pair<int,int>
#define PLL pair<LL,LL>
#define MP make_pair
#define F first
#define S second
#define INF INT_MAX

inline void optimizeIO()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
}

const int nmax = 1e6+7;
const LL LINF = 1e17;

string to_str(LL x)
{
    stringstream ss;
    ss<<x;
    return ss.str();
}

LL nCr[30][30];
int cnt[30];
int len;


LL count_perm(int n)
{
    LL ret = 1;

    for (int i = 0; i < 26; i++)
    {
        ret *= nCr[n][cnt[i]];
        n -= cnt[i];

    }
    return ret;
}

LL solve(int pos,int rem)
{
    if(pos>=len)
        return 0;

    int i;

    for(i=0;i<26;i++)
    {
        if(cnt[i])
        {
            cnt[i]--;

            LL use = count_perm(len-pos-1);

            //cout<<i<<"  -->  "<<use<<endl;

            if(use>=rem)
                break;

            cnt[i]++;
            rem -= use;
        }
    }

    cout<<char(i+'a');

    solve(pos+1,rem);
}

int main()
{
    for(int i=0; i<=20; i++)
    {
        nCr[i][0]=1;
        nCr[i][i]=1;
        for(int j=1; j<=i; j++)
        {
            nCr[i][j]=nCr[i-1][j]+nCr[i-1][j-1];
        }
    }

    int tc;
    cin>>tc;

    for(int q=1; q<=tc; q++)
    {

        memset(cnt,0,sizeof cnt);

        string s;
        int nth;
        cin>>s>>nth;

        len = s.size();

        for(int i=0; i<len; i++)
            cnt[s[i]-'a']++;

        cout<<"Case "<<q<<": ";

        if(count_perm(len)<nth)
        {
            cout<<"Impossible";
        }
        else
            solve(0,nth);

        cout<<endl;

    }

    return 0;
}

```