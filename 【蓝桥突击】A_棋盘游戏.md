## 【蓝桥突击】A_棋盘游戏

[原题搁这呢](https://vjudge.net/contest/65959#problem/A)

在一个给定形状的棋盘（形状可能是不规则的）上面摆放棋子，棋子没有区别。要求摆放时任意的两个棋子不能放在棋盘中的同一行或者同一列，请编程求解对于给定形状和大小的棋盘，摆放k个棋子的所有可行的摆放方案C。

Input

输入含有多组测试数据。
每组数据的第一行是两个正整数，n k，用一个空格隔开，表示了将在一个n*n的矩阵内描述棋盘，以及摆放棋子的数目。 n <= 8 , k <= n
当为-1 -1时表示输入结束。
随后的n行描述了棋盘的形状：每行有n个字符，其中 # 表示棋盘区域， . 表示空白区域（数据保证不出现多余的空白行或者空白列）。

Output

对于每一组数据，给出一行输出，输出摆放的方案数目C （数据保证C<2^31）。

Sample

**Input**

2 1
#.
.#
4 4
...#
..#.
.#..
#...
-1 -1

**Output**

2
1

思路：典中典之比八皇后还入门的dfs

逐行搜索，通过一维数组标记某列是否可放即可，注意存在某一行全不放的情况，多搜一遍。

```c++
#include<iostream>//tnnd,为什么不让用bits，为什么！！！
#include<cstring>
#define rep(i,a,b) for(int i=a;i<=b;i++)//
using namespace std;
int ans,n,k;
char s[9][9];
bool st[9];//用于标记列，逐行搜索自动表示标记行
void dfs(int step,int m){
	if(!m){
		ans++;
		return;
	}
	if(step>n){
		return;
	}
	rep(i,1,n){
		if(!st[i]&&s[step][i]=='#'){
			st[i]=1;
			dfs(step+1,m-1);
			st[i]=0;
		}
	}
	dfs(step+1,m);//这一行跳过的情况
}
signed main(){
	while(cin>>n>>k&&n>=0){
		memset(st,0,sizeof st);//
		rep(i,1,n){
			rep(j,1,n){
				cin>>s[i][j];
			}
		}
		ans=0;
		dfs(1,k);
		cout<<ans<<endl;
	}
	return 0;
}
```

