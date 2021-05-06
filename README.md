# application_of_topo_sort
Assign directions to edges so that the directed graph remains acyclic
// c++ code
#include <iostream>
#include<vector>
#include<bits/stdc++.h>
using namespace std;
void topo(int v,vector<int>adj[],vector<bool>&vis,stack<int>&st)
{
    vis[v]=true;
    for(auto nbr : adj[v])
    {
        if(!vis[nbr])
         topo(nbr,adj,vis,st);
    }
    st.push(v);
}
int idx(vector<int>res,int s)
{
    int n=res.size();
    for(int i=0;i<n;i++)
    {
        if(res[i]==s)
         return i;
    }
}
int main()
{
    int v,e;
    cin>>v>>e;
    std::vector<int>adj[v] ;
    for(int i=0;i<e;i++)
     {
         int s,d;
         cin>>s>>d;
         adj[s].push_back(d);
     }
     vector<bool>vis(v,false);
     std::stack<int>st ;
     for(int i=0;i<v;i++)
      if(!vis[i])
       topo(i,adj,vis,st);
      
      vector<int>store;
      while(!st.empty())
      {
          int node=st.top();
          st.pop();
          store.push_back(node);
      }
      for(auto pr : store)
      {
        std::cout <<pr<<"   ";
      }
      cout<<endl;
      int n;
      cin>>n;
      while(n--)
      {
          int s,d;
          cin>>s>>d;
          int idx1=idx(store,s);
          int idx2=idx(store,d);
          if(idx1>idx2)
           cout<<d<<"-->"<<s<<endl;
          else
           cout<<s<<"-->"<<d<<endl;
      }
      return 0;
}
/* input
6 10
0 1
0 5
1 2
1 3
1 4
2 3
2 4
3 4
5 1
5 2
4
0 2
0 3
4 5
3 5
*/
