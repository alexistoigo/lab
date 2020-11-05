[String]

# Árvore de sufixo

Este algoritmo constrói uma árvore de sufixos para uma determinada string ***s*** de comprimento ***n*** em ***O ( n * log( k ) )***, onde **k** é o tamanho do alfabeto (se **k** é considerada uma constante, o comportamento assintótico é linear).

A entrada para o algoritmo é a string ***s*** e seu comprimento ***n***, que são passados como variáveis globais.

A função principal ***build_tree*** constrói uma árvore de sufixos. Ele é armazenado como uma série de estruturas ***node***, onde ***node[0]*** está a raiz da árvore.

Para simplificar o código, as arestas são armazenadas nas mesmas estruturas: para cada vértice sua estrutura ***node*** armazena a informação sobre a aresta entre ele e seu pai. No geral, cada um ***node*** armazena as seguintes informações:

- ***(l, r)*** - limites esquerdo e direito da substring ***s[l..r-1]*** que correspondem à aresta para este nó;
- ***par*** - o nó pai;
- ***link*** - o link de sufixo;
- ***next*** - a lista de arestas saindo deste nó.

### Implementação
 ````cpp
string s;
int n;

struct node {
    int l, r, par, link;
    map<char,int> next;

    node (int l=0, int r=0, int par=-1)
        : l(l), r(r), par(par), link(-1) {}
    int len()  {  return r - l;  }
    int &get (char c) {
        if (!next.count(c))  next[c] = -1;
        return next[c];
    }
};
node t[MAXN];
int sz;

struct state {
    int v, pos;
    state (int v, int pos) : v(v), pos(pos)  {}
};
state ptr (0, 0);

state go (state st, int l, int r) {
    while (l < r)
        if (st.pos == t[st.v].len()) {
            st = state (t[st.v].get( s[l] ), 0);
            if (st.v == -1)  return st;
        }
        else {
            if (s[ t[st.v].l + st.pos ] != s[l])
                return state (-1, -1);
            if (r-l < t[st.v].len() - st.pos)
                return state (st.v, st.pos + r-l);
            l += t[st.v].len() - st.pos;
            st.pos = t[st.v].len();
        }
    return st;
}

int split (state st) {
    if (st.pos == t[st.v].len())
        return st.v;
    if (st.pos == 0)
        return t[st.v].par;
    node v = t[st.v];
    int id = sz++;
    t[id] = node (v.l, v.l+st.pos, v.par);
    t[v.par].get( s[v.l] ) = id;
    t[id].get( s[v.l+st.pos] ) = st.v;
    t[st.v].par = id;
    t[st.v].l += st.pos;
    return id;
}

int get_link (int v) {
    if (t[v].link != -1)  return t[v].link;
    if (t[v].par == -1)  return 0;
    int to = get_link (t[v].par);
    return t[v].link = split (go (state(to,t[to].len()), t[v].l + (t[v].par==0), t[v].r));
}

void tree_extend (int pos) {
    for(;;) {
        state nptr = go (ptr, pos, pos+1);
        if (nptr.v != -1) {
            ptr = nptr;
            return;
        }

        int mid = split (ptr);
        int leaf = sz++;
        t[leaf] = node (pos, n, mid);
        t[mid].get( s[pos] ) = leaf;

        ptr.v = get_link (mid);
        ptr.pos = t[ptr.v].len();
        if (!mid)  break;
    }
}

void build_tree() {
    sz = 1;
    for (int i=0; i<n; ++i)
        tree_extend (i);
} 
````

Para obter uma descrição do algoritmo, consulte outras fontes, como [Algorithms on Strings, Trees, and Sequences] de Dan Gusfield.

[String]: https://github.com/alexistoigo/lab/blob/master/Processamento%20de%20String/main.md#processamento-de-string
[Algorithms on Strings, Trees, and Sequences]: http://web.stanford.edu/~mjkay/gusfield.pdf

