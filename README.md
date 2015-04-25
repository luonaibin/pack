# pack
背包问题九讲
#include <iostream>
using namespace std;

const int N = 3;//物品个数
const int V = 5;//背包最大容量
int weight[N + 1] = {0,3,2,2};//物品重量
int value[N + 1] = {0,5,10,20};//物品价值

int f[N + 1][V + 1] = {{0}};

int Max(int x,int y)
{
	return x > y ? x : y;
}

/*
目标：在不超过背包容量的情况下，最多能获得多少价值

子问题状态:f[i][j]:表示前i件物品放入容量为j的背包得到的最大价值

状态转移方程:f[i][j] = max{f[i - 1][j],f[i - 1][j - weight[i]] + value[i]}

初始化:f数组全设置为0
*/
int Knapsack()
{
	//初始化
	memset(f,0,sizeof(f));
	//递推
	for (int i = 1;i <= N;i++) //枚举物品
	{
		for (int j = 0;j <= V;j++) //枚举背包容量
		{
			f[i][j] = f[i - 1][j];
			if (j >= weight[i])
			{
				f[i][j] = Max(f[i - 1][j],f[i - 1][j - weight[i]] + value[i]);
			}
		}
	}
	return f[N][V];
}

int main()
{
	cout<<Knapsack()<<endl;
	system("pause");
	return 1;
}
