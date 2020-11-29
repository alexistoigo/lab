[Geometria]

# Intersecção de segmentos

Você recebe dois segmentos (a, b) e (c,d). Você tem que verificar se eles se cruzam. Claro, você pode encontrar sua interseção e verificar se não está vazia, mas isso não pode ser feito em inteiros para segmentos com coordenadas inteiras. A abordagem descrita aqui pode funcionar em inteiros.

Em primeiro lugar, considere o caso em que os segmentos fazem parte da mesma linha. Neste caso, basta verificar se suas projeções sobreO x e O yse cruzam. No outro caso a e b não deve estar do mesmo lado da linha (c , d), e c e d não deve estar do mesmo lado da linha (a , b). Isso pode ser verificado com alguns produtos cruzados.

```cpp
struct pt {
    long long x, y;
    pt() {}
    pt(long long _x, long long _y) : x(_x), y(_y) {}
    pt operator-(const pt& p) const { return pt(x - p.x, y - p.y); }
    long long cross(const pt& p) const { return x * p.y - y * p.x; }
    long long cross(const pt& a, const pt& b) const { return (a - *this).cross(b - *this); }
};

int sgn(const long long& x) { return x >= 0 ? x ? 1 : 0 : -1; }

bool inter1(long long a, long long b, long long c, long long d) {
    if (a > b)
        swap(a, b);
    if (c > d)
        swap(c, d);
    return max(a, c) <= min(b, d);
}

bool check_inter(const pt& a, const pt& b, const pt& c, const pt& d) {
    if (c.cross(a, d) == 0 && c.cross(b, d) == 0)
        return inter1(a.x, b.x, c.x, d.x) && inter1(a.y, b.y, c.y, d.y);
    return sgn(a.cross(b, c)) != sgn(a.cross(b, d)) &&
           sgn(c.cross(d, a)) != sgn(c.cross(d, b));
}

```

[Geometria]: https://github.com/alexistoigo/lab/blob/master/Geometria/main.md#geometria
