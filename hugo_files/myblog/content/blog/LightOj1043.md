+++
title = "LightOj 1043 (Triangle Partitioning)"
date = "2018-11-20"
author = "~5 min read"
tags = ["lightoj", "cp", "problem solving" ,"binary search" ,"geometry"]
description = "Triangle Partitioning"
+++

# Idea 1
---
Binary Search  
- AB/AD = AC/AE = BC/DE
- So  , AE = (AC*AD)/AB  
  and , DE = (BC*AD)/AB
- The area ratio of those two triangles can be calculated as a function of AD .  
So, we can Binary Search over AD

# Idea 2 
---
Geometry
- AB/AD = AC/AE = BC/DE
- We know that , If two triangles are similar, then the ratio of the area of both triangles is proportional to the square of the ratio of their corresponding sides.  
- So , Area(ABC)/Area(ADE) = (AB/AD)^2 = (AC/AE)^2 = (BC/DE)^2


| *Idea 1 `code`* |
| --------------- |
```cpp

/** Which of the favors of your Lord will you deny ?* */

#include<bits/stdc++.h>
using namespace std;

double triangleRatio (double ab,double ac,double bc,double ad)
{
    double ae=(ac*ad)/ab, de=(bc*ad)/ab,s1,s2;

    s1 = (ab+ac+bc)/2.0;
    s2 = (ad+ae+de)/2.0;

    double areaBig = sqrt(s1 * (s1-ab) * (s1-ac) * (s1-bc));
    double areaSmall = sqrt(s2 * (s2-ad) * (s2-ae) * (s2-de));

    double areaTrap = areaBig-areaSmall;

    double ratio = areaSmall/areaTrap;

    return ratio;

}

double BS(double ab,double ac,double bc,double ratio)
{
    double low, high, mid,ad ;

    low = 0.0;
    high = ab;

    for(int i=0; i<100; i++)
    {
        mid = (low + high)/2.0;
        ad = mid;
        if(triangleRatio(ab,ac,bc,ad)>ratio)
            high = mid ;
        else
            low = mid;

    }
    return ad ;
}

int main()
{
    int n;
    scanf("%d",&n);

    for(int i=1; i<=n; i++)
    {
        double ab,bc,ac,ratio;
        scanf("%lf %lf %lf %lf",&ab,&bc,&ac,&ratio);

        printf("Case %d: %lf\n",i,BS(ab,bc,ac,ratio));

    }

    return 0;
}

```

| *Idea 2 `code`* |
| --------------- |

```cpp
/** Which of the favors of your Lord will you deny ?* */

#include<bits/stdc++.h>
using namespace std;

int main()
{
    int n;
    scanf("%d",&n);

    for(int i=1;i<=n;i++)
    {
        double ab,bc,ac,x;
        scanf("%lf %lf %lf %lf",&ab,&ac,&bc,&x);

        double k = sqrt((1+x)/x);

        printf("Case %d: %.10lf\n",i,ab/k);

    }

    return 0;
}
```