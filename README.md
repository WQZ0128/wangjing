# wangjing
这是算法程序，包括0-1背包，元素选择，最小生成树。
#include <iostream>
using namespace std;
#define n 5 
#define C 100 
int P[n+1][C+1], Rec[n+1][C+1];
void knapsack(int p[], int v[]) 
{
    for (int i = 0; i <= C; i++) 
    {
        P[0][i] = 0;
    }
    for (int i = 0; i <= n; i++) 
    {
        P[i][0] = 0;
    }
    for (int i = 1; i <= n; i++)
    {
        for (int c = 1; c <= C; c++)
        {
            if (v[i] <= c &&
                p[i] + P[i-1][c-v[i]] > P[i-1][c])
            {
                P[i][c] = p[i] + P[i-1][c-v[i]];
                Rec[i][c] = 1;
            }
            else
            {
                P[i][c] = P[i-1][c];
                Rec[i][c] = 0;
            }
        }
    }
    int K = C;
    for (int i = 1; i <=n; i++)
    {
        if (Rec[i][K] == 1)
        {
            cout << "选择商品" << i << endl;
            K = K - v[i];
        }
        else
        {
            cout << "不选商品" << i << endl;
        }
    }
    cout << "最大价值为" << P[n][C] << endl;
}
int main()
{
    int p[n+1] = {0, 50, 200, 180, 225, 200}; 
    int v[n+1] = {0, 5, 25, 30, 45, 50}; 
    cout << "************0-1背包问题************" << endl;
    knapsack(p, v);
}
