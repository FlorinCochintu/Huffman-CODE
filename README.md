# Huffman-CODE
#include <stdio.h>
 
using namespace std;
 
#define maxn 5000100
#define inf 1LL * 1000000000 * 1000000000
 
struct nod
{
    long long v;
    long f[2];
} nod[2*maxn];
 
long n, i, j, k, p, l, r;
long long b[maxn], m, sol;
long f[maxn], lg[maxn];
 
void df(long poz, long long cod, long nivel)
{
    if(nod[poz].f[0])
    {
        df(nod[poz].f[0], cod*2, nivel+1);
        df(nod[poz].f[1], cod*2+1, nivel+1);
        return;
    }
    lg[poz]=nivel;
    b[poz]=cod;
}
 
void solve()
{
    l=1;
    r=n;
    for(l=n-1; l; l--)
    {
        ++r;
        for(i=0; i<2; i++)
        {
            p=0;
            m=inf;
            for(j=1; j<r; j++)
            {
                if(nod[j].v<m && !f[j])
                {
                    p=j;
                    m=nod[j].v;
                }
            }
            f[p]=1;
            nod[r].f[i]=p;
            nod[r].v+=nod[p].v;
        }
        sol+=nod[r].v;
    }
    df(r, 0, 0);
}             
 
int main()
{
    freopen("huffman.in", "r", stdin);
    freopen("huffman.out", "w", stdout);
    scanf("%d", &n);
    for(i=1; i<=n; i++)
    {
        scanf("%d", &nod[i].v);
    }
    solve();
    printf("%lld\n", sol);
    for(i=1; i<=n; i++)
    {
        printf("%d %lld\n", lg[i], b[i]);
    }
    return 0;
}
