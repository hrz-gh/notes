# 代码

## 快速幂

```cpp
LL iterPower(LL a, LL b, LL m) {
    if(a >= m) a %= m;
    LL ans = 1;
    for(; b; b >>= 1) {
        if(b&1) ans = ans*a%m;
        a = a*a%m;
    }
    return ans;
}
```



## 斐波那契数列

```cpp
__int64 fibI ( int n ) { //计算Fibonacci数列的第n项（迭代版）：O(n)
   __int64 f = 1, g = 0; //初始化：fib(-1)、fib(0)
   while ( 0 < n-- ) { g += f; f = g - f; } //依据原始定义，通过n次加法和减法计算fib(n)
   return g; //返回
}
```

## 二分查找

```cpp
// 二分查找算法（版本C）：在有序向量的区间[lo, hi)内查找元素e，0 <= lo <= hi <= _size
template <typename T> static Rank binSearch ( T* S, T const& e, Rank lo, Rank hi ) {
   /*DSA*/printf ( "BIN search (C)\n" );
   while ( lo < hi ) { //每步迭代仅需做一次比较判断，有两个分支
      /*DSA*/ //for ( int i = 0; i < lo; i++ ) printf ( "     " ); if ( lo >= 0 ) for ( int i = lo; i < hi; i++ ) printf ( "....^" ); printf ( "\n" );
      Rank mi = ( lo + hi ) >> 1; //以中点为轴点（区间宽度的折半，等效于宽度之数值表示的右移）
      ( e < S[mi] ) ? hi = mi : lo = mi + 1; //经比较后确定深入[lo, mi)或(mi, hi)
   } //成功查找不能提前终止
   /*DSA*/ //for ( int i = 0; i < lo - 1; i++ ) printf ( "     " ); if ( lo > 0 ) printf ( "....|\n" ); else printf ( "<<<<|\n" );
   return lo - 1; //循环结束时，lo为大于e的元素的最小秩，故lo - 1即不大于e的元素的最大秩
} //有多个命中元素时，返回秩最大者；查找失败时，能够返回失败的位置
```

## 迭代版二叉树遍历

```cpp
// 先序遍历
//从当前节点出发，沿左分支不断深入，直至没有左分支的节点；沿途节点遇到后立即访问
template <typename T, typename VST> //元素类型、操作器
static void visitAlongVine ( BinNodePosi<T> x, VST& visit, Stack<BinNodePosi<T>>& S ) {
   while ( x ) {
      visit ( x->data ); //访问当前节点
      S.push ( x->rc ); //右孩子入栈暂存（可优化：通过判断，避免空的右孩子入栈）
      x = x->lc;  //沿左分支深入一层
   }
}

template <typename T, typename VST> //元素类型、操作器
void travPre_I2 ( BinNodePosi<T> x, VST& visit ) { //二叉树先序遍历算法（迭代版#2）
   Stack<BinNodePosi<T>> S; //辅助栈
   while ( true ) {
      visitAlongVine ( x, visit, S ); //从当前节点出发，逐批访问
      if ( S.empty() ) break; //直到栈空
      x = S.pop(); //弹出下一批的起点
   }
}
```

```cpp
// 中序遍历

template <typename T> BinNodePosi<T> BinNode<T>::succ() { //定位节点v的直接后继
   BinNodePosi<T> s = this; //记录后继的临时变量
   if ( rc ) { //若有右孩子，则直接后继必在右子树中，具体地就是
      s = rc; //右子树中
      while ( HasLChild ( *s ) ) s = s->lc; //最靠左（最小）的节点
   } else { //否则，直接后继应是“将当前节点包含于其左子树中的最低祖先”，具体地就是
      while ( IsRChild ( *s ) ) s = s->parent; //逆向地沿右向分支，不断朝左上方移动
      s = s->parent; //最后再朝右上方移动一步，即抵达直接后继（如果存在）
   }
   return s;
}

template <typename T, typename VST>
void travIn ( BinNodePosi<T> x, VST& visit ) {
    while ( HasLChild ( *x ) ) x = x->lc;
    while ( x ) {
        visit ( x->data );
        x = x->succ();
    }
    return;
}
```

```cpp
// 后序遍历
template <typename T> //在以S栈顶节点为根的子树中，找到最高左侧可见叶节点
static void gotoLeftmostLeaf ( Stack<BinNodePosi<T>>& S ) { //沿途所遇节点依次入栈
   while ( BinNodePosi<T> x = S.top() ) //自顶而下，反复检查当前节点（即栈顶）
      if ( HasLChild ( *x ) ) { //尽可能向左
         if ( HasRChild ( *x ) ) S.push ( x->rc ); //若有右孩子，优先入栈
         S.push ( x->lc ); //然后才转至左孩子
      } else //实不得已
         S.push ( x->rc ); //才向右
   S.pop(); //返回之前，弹出栈顶的空节点
}

template <typename T, typename VST>
void travPost_I ( BinNodePosi<T> x, VST& visit ) { //二叉树的后序遍历（迭代版）
   Stack<BinNodePosi<T>> S; //辅助栈
   if ( x ) S.push ( x ); //根节点入栈
   while ( !S.empty() ) { //x始终为当前节点
      if ( S.top() != x->parent ) ////若栈顶非x之父（而为右兄）
         gotoLeftmostLeaf ( S ); //则在其右兄子树中找到HLVFL（相当于递归深入）
      x = S.pop(); visit ( x->data ); //弹出栈顶（即前一节点之后继），并访问之
   }
}
```

## 图的遍历

```cpp
// 遍历
template <typename Tv, typename Te> template <typename PU> //优先级搜索（全图）
void Graph<Tv, Te>::pfs ( int s, PU prioUpdater ) { //assert: 0 <= s < n
   reset(); int v = s; //初始化
   do //逐一检查所有顶点
      if ( UNDISCOVERED == status ( v ) ) //一旦遇到尚未发现的顶点
         PFS ( v, prioUpdater ); //即从该顶点出发启动一次PFS
   while ( s != ( v = ( ++v % n ) ) ); //按序号检查，故不漏不重
}

template <typename Tv, typename Te> template <typename PU> //顶点类型、边类型、优先级更新器
void Graph<Tv, Te>::PFS ( int s, PU prioUpdater ) { //优先级搜索（单个连通域）
   priority ( s ) = 0; status ( s ) = VISITED; parent ( s ) = -1; //初始化，起点s加至PFS树中
   while ( 1 ) { //将下一顶点和边加至PFS树中
      for ( int w = firstNbr ( s ); -1 < w; w = nextNbr ( s, w ) ) //枚举s的所有邻居w
         prioUpdater ( this, s, w ); //更新顶点w的优先级及其父顶点
      for ( int shortest = INT32_MAX, w = 0; w < n; w++ )
         if ( UNDISCOVERED == status ( w ) ) //从尚未加入遍历树的顶点中
            if ( shortest > priority ( w ) ) //选出下一个
               { shortest = priority ( w ); s = w; } //优先级最高的顶点s
      if ( VISITED == status ( s ) ) break; //直至所有顶点均已加入
      status ( s ) = VISITED; type ( parent ( s ), s ) = TREE; //将s及与其父的联边加入遍历树
   }
} //通过定义具体的优先级更新策略prioUpdater，即可实现不同的算法功能

template <typename Tv, typename Te> struct DfsPU { //针对DFS算法的顶点优先级更新器
   virtual void operator() ( Graph<Tv, Te>* g, int uk, int v ) {
      if ( g->status ( v ) == UNDISCOVERED ) //对于uk每一尚未被发现的邻接顶点v
         if ( g->priority ( v ) > g->priority ( uk ) - 1 ) { //将其到起点距离的负数作为优先级数
            g->priority ( v ) = g->priority ( uk ) - 1; //更新优先级（数）
            g->parent ( v ) = uk; //更新父节点
            return; //注意：与BfsPU()不同，这里只要有一个邻接顶点可更新，即可立即返回
         } //如此效果等同于，后被发现者优先
   }
};

// BFS 等效于权值为1的dijkstra
template <typename Tv, typename Te> struct DijkPU { //针对Dijkstra算法的顶点优先级更新器
   virtual void operator() ( Graph<Tv, Te>* g, int uk, int v ) {
      if ( UNDISCOVERED == g->status ( v ) ) //对于uk每一尚未被发现的邻接顶点v，按Dijkstra策略
         if ( g->priority ( v ) > g->priority ( uk ) + g->weight ( uk, v ) ) { //做松弛
            g->priority ( v ) = g->priority ( uk ) + g->weight ( uk, v ); //更新优先级（数）
            g->parent ( v ) = uk; //并同时更新父节点
         }
   }
};

template <typename Tv, typename Te> struct PrimPU { //针对Prim算法的顶点优先级更新器
   virtual void operator() ( Graph<Tv, Te>* g, int uk, int v ) {
      if ( UNDISCOVERED == g->status ( v ) ) //对于uk每一尚未被发现的邻接顶点v
         if ( g->priority ( v ) > g->weight ( uk, v ) ) { //按Prim策略做松弛
            g->priority ( v ) = g->weight ( uk, v ); //更新优先级（数）
            g->parent ( v ) = uk; //更新父节点
         }
   }
};
```

## 图的双连通域分解

同一分支中`dtime[v]`越小意味着越高，且每个节点只有唯一的`dtime[v]`故使用`dtime[v]`更新`hca[v]`。
```cpp
template <typename Tv, typename Te> void Graph<Tv, Te>::bcc ( int s ) { //基于DFS的BCC分解算法
   reset(); int clock = 0; int v = s; Stack<int> S; //栈S用以记录已访问的顶点
   do
      if ( UNDISCOVERED == status ( v ) ) { //一旦发现未发现的顶点（新连通分量）
         BCC ( v, clock, S ); //即从该顶点出发启动一次BCC
         S.pop(); //遍历返回后，弹出栈中最后一个顶点——当前连通域的起点
      }
   while ( s != ( v = ( ++v % n ) ) );
}
#define hca(x) (fTime(x)) //利用此处闲置的fTime[]充当hca[]
template <typename Tv, typename Te> //顶点类型、边类型
void Graph<Tv, Te>::BCC ( int v, int& clock, Stack<int>& S ) { //assert: 0 <= v < n
   hca ( v ) = dTime ( v ) = ++clock; status ( v ) = DISCOVERED; S.push ( v ); //v被发现并入栈
   for ( int u = firstNbr ( v ); -1 < u; u = nextNbr ( v, u ) ) //枚举v的所有邻居u
      switch ( status ( u ) ) { //并视u的状态分别处理
         case UNDISCOVERED:
            parent ( u ) = v; type ( v, u ) = TREE; BCC ( u, clock, S ); //从顶点u处深入
            if ( hca ( u ) < dTime ( v ) ) //遍历返回后，若发现u（通过后向边）可指向v的真祖先
               hca ( v ) = min ( hca ( v ), hca ( u ) ); //则v亦必如此
            else //否则，以v为关节点（u以下即是一个BCC，且其中顶点此时正集中于栈S的顶部）
               /*DSA*/{
               /*DSA*/printf ( "BCC rooted at %c:", vertex ( v ) );
               /*DSA*/Stack<int> temp; do { temp.push ( S.pop() ); print ( vertex ( temp.top() ) ); } while ( u != temp.top() ); print( vertex ( parent(u) ) ); while ( !temp.empty() ) S.push ( temp.pop() );
               while ( u != S.pop() ); //弹出当前BCC中（除v外）的所有节点，可视需要做进一步处理
               /*DSA*/printf ( "\n" );
               /*DSA*/}
            break;
         case DISCOVERED:
            type ( v, u ) = BACKWARD; //标记(v, u)，并按照“越小越高”的准则
            if ( u != parent ( v ) ) hca ( v ) = min ( hca ( v ), dTime ( u ) ); //更新hca[v]
            break;
         default: //VISITED (digraphs only)
            type ( v, u ) = ( dTime ( v ) < dTime ( u ) ) ? FORWARD : CROSS;
            break;
      }
   status ( v ) = VISITED; //对v的访问结束
}
```

## BST

节点删除

```cpp
template <typename T>
static BinNodePosi<T> removeAt ( BinNodePosi<T> & x, BinNodePosi<T> & hot ) {
   BinNodePosi<T> w = x; //实际被摘除的节点，初值同x
   BinNodePosi<T> succ = NULL; //实际被删除节点的接替者
   if ( !HasLChild ( *x ) ) //若*x的左子树为空，则可
      succ = x = x->rc; //直接将*x替换为其右子树
   else if ( !HasRChild ( *x ) ) //若右子树为空，则可
      succ = x = x->lc; //对称地处理——注意：此时succ != NULL
   else { //若左右子树均存在，则选择x的直接后继作为实际被摘除节点，为此需要
      w = w->succ(); //（在右子树中）找到*x的直接后继*w
      swap ( x->data, w->data ); //交换*x和*w的数据元素
      BinNodePosi<T> u = w->parent;
      ( ( u == x ) ? u->rc : u->lc ) = succ = w->rc; //隔离节点*w
   }
   hot = w->parent; //记录实际被删除节点的父亲
   if ( succ ) succ->parent = hot; //并将被删除节点的接替者与hot相联
   release ( w->data ); release ( w ); return succ; //释放被摘除节点，返回接替者
}
```


基于“3+4”重构的重平衡

```cpp
template <typename T> BinNodePosi<T> BST<T>::rotateAt ( BinNodePosi<T> v ) { //v为非空孙辈节点
   /*DSA*/if ( !v ) { printf ( "\a\nFail to rotate a null node\n" ); exit ( -1 ); }
   BinNodePosi<T> p = v->parent; BinNodePosi<T> g = p->parent; //视v、p和g相对位置分四种情况
   if ( IsLChild ( *p ) ) /* zig */
      if ( IsLChild ( *v ) ) { /* zig-zig */ //*DSA*/printf("\tzIg-zIg: ");
         p->parent = g->parent; //向上联接
         return connect34 ( v, p, g, v->lc, v->rc, p->rc, g->rc );
      } else { /* zig-zag */  //*DSA*/printf("\tzIg-zAg: ");
         v->parent = g->parent; //向上联接
         return connect34 ( p, v, g, p->lc, v->lc, v->rc, g->rc );
      }
   else  /* zag */
      if ( IsRChild ( *v ) ) { /* zag-zag */ //*DSA*/printf("\tzAg-zAg: ");
         p->parent = g->parent; //向上联接
         return connect34 ( g, p, v, g->lc, p->lc, v->lc, v->rc );
      } else { /* zag-zig */  //*DSA*/printf("\tzAg-zIg: ");
         v->parent = g->parent; //向上联接
         return connect34 ( g, v, p, g->lc, v->lc, v->rc, p->rc );
      }
}
```

## splay tree

双层伸展

```   cpp
template <typename NodePosi> inline //在节点*p与*lc（可能为空）之间建立父（左）子关系
void attachAsLC ( NodePosi lc, NodePosi p ) { p->lc = lc; if ( lc ) lc->parent = p; }

template <typename NodePosi> inline //在节点*p与*rc（可能为空）之间建立父（右）子关系
void attachAsRC ( NodePosi p, NodePosi rc ) { p->rc = rc; if ( rc ) rc->parent = p; }

template <typename T> //Splay树伸展算法：从节点v出发逐层伸展
BinNodePosi<T> Splay<T>::splay ( BinNodePosi<T> v ) { //v为因最近访问而需伸展的节点位置
   if ( !v ) return NULL; BinNodePosi<T> p; BinNodePosi<T> g; //*v的父亲与祖父
   while ( ( p = v->parent ) && ( g = p->parent ) ) { //自下而上，反复对*v做双层伸展
      BinNodePosi<T> gg = g->parent; //每轮之后*v都以原曾祖父（great-grand parent）为父
      if ( IsLChild ( *v ) )
         if ( IsLChild ( *p ) ) { //zig-zig
            /*DSA*/printf ( "\tzIg-zIg :" ); print ( g ); print ( p ); print ( v ); printf ( "\n" );
            attachAsLC ( p->rc, g ); attachAsLC ( v->rc, p );
            attachAsRC ( p, g ); attachAsRC ( v, p );
         } else { //zig-zag
            /*DSA*/printf ( "\tzIg-zAg :" ); print ( g ); print ( p ); print ( v ); printf ( "\n" );
            attachAsLC ( v->rc, p ); attachAsRC ( g, v->lc );
            attachAsLC ( g, v ); attachAsRC ( v, p );
         }
      else if ( IsRChild ( *p ) ) { //zag-zag
         /*DSA*/printf ( "\tzAg-zAg :" ); print ( g ); print ( p ); print ( v ); printf ( "\n" );
         attachAsRC ( g, p->lc ); attachAsRC ( p, v->lc );
         attachAsLC ( g, p ); attachAsLC ( p, v );
      } else { //zag-zig
         /*DSA*/printf ( "\tzAg-zIg :" ); print ( g ); print ( p ); print ( v ); printf ( "\n" );
         attachAsRC ( p, v->lc ); attachAsLC ( v->rc, g );
         attachAsRC ( v, g ); attachAsLC ( p, v );
      }
      if ( !gg ) v->parent = NULL; //若*v原先的曾祖父*gg不存在，则*v现在应为树根
      else //否则，*gg此后应该以*v作为左或右孩子
         ( g == gg->lc ) ? attachAsLC ( v, gg ) : attachAsRC ( gg, v );
      updateHeight ( g ); updateHeight ( p ); updateHeight ( v );
   } //双层伸展结束时，必有g == NULL，但p可能非空
   if ( p = v->parent ) { //若p果真非空，则额外再做一次单旋
      /*DSA*/if ( IsLChild ( *v ) ) { printf ( "\tzIg :" ); print ( p ); print ( v ); printf ( "\n" ); }
      /*DSA*/else              { printf ( "\tzAg :" ); print ( p ); print ( v ); printf ( "\n" ); }
      if ( IsLChild ( *v ) ) { attachAsLC ( v->rc, p ); attachAsRC ( v, p ); }
      else                   { attachAsRC ( p, v->lc ); attachAsLC ( p, v ); }
      updateHeight ( p ); updateHeight ( v );
   }
   v->parent = NULL; return v;
} //调整之后新树根应为被伸展的节点，故返回该节点的位置以便上层函数更新树根
```

## B-树

上溢

```cpp
template <typename T> //关键码插入后若节点上溢，则做节点分裂处理
void BTree<T>::solveOverflow ( BTNodePosi<T> v ) {
   if ( _order >= v->child.size() ) return; //递归基：当前节点并未上溢
   Rank s = _order / 2; //轴点（此时应有_order = key.size() = child.size() - 1）
   BTNodePosi<T> u = new BTNode<T>(); //注意：新节点已有一个空孩子
   for ( Rank j = 0; j < _order - s - 1; j++ ) { //v右侧_order-s-1个孩子及关键码分裂为右侧节点u
      u->child.insert ( j, v->child.remove ( s + 1 ) ); //逐个移动效率低
      u->key.insert ( j, v->key.remove ( s + 1 ) ); //此策略可改进
   }
   u->child[_order - s - 1] = v->child.remove ( s + 1 ); //移动v最靠右的孩子
   if ( u->child[0] ) //若u的孩子们非空，则
      for ( Rank j = 0; j < _order - s; j++ ) //令它们的父节点统一
         u->child[j]->parent = u; //指向u
   BTNodePosi<T> p = v->parent; //v当前的父节点p
   if ( !p ) { _root = p = new BTNode<T>(); p->child[0] = v; v->parent = p; } //若p空则创建之
   Rank r = 1 + p->key.search ( v->key[0] ); //p中指向v的指针的秩
   p->key.insert ( r, v->key.remove ( s ) ); //轴点关键码上升
   p->child.insert ( r + 1, u );  u->parent = p; //新节点u与父节点p互联
   solveOverflow ( p ); //上升一层，如有必要则继续分裂——至多递归O(logn)层
}
```

下溢

```cpp
template <typename T> //关键码删除后若节点下溢，则做节点旋转或合并处理
void BTree<T>::solveUnderflow ( BTNodePosi<T> v ) {
   if ( ( _order + 1 ) / 2 <= v->child.size() ) return; //递归基：当前节点并未下溢
   BTNodePosi<T> p = v->parent;
   if ( !p ) { //递归基：已到根节点，没有孩子的下限
      if ( !v->key.size() && v->child[0] ) {
         //但倘若作为树根的v已不含关键码，却有（唯一的）非空孩子，则
         /*DSA*/printf ( "collapse\n" );
         _root = v->child[0]; _root->parent = NULL; //这个节点可被跳过
         v->child[0] = NULL; release ( v ); //并因不再有用而被销毁
      } //整树高度降低一层
      return;
   }
   Rank r = 0; while ( p->child[r] != v ) r++;
   //确定v是p的第r个孩子——此时v可能不含关键码，故不能通过关键码查找
   //另外，在实现了孩子指针的判等器之后，也可直接调用Vector::find()定位
   /*DSA*/printf ( "\nrank = %d", r );
// 情况1：向左兄弟借关键码
   if ( 0 < r ) { //若v不是p的第一个孩子，则
      BTNodePosi<T> ls = p->child[r - 1]; //左兄弟必存在
      if ( ( _order + 1 ) / 2 < ls->child.size() ) { //若该兄弟足够“胖”，则
         /*DSA*/printf ( " ... case 1\n" );
         v->key.insert ( 0, p->key[r - 1] ); //p借出一个关键码给v（作为最小关键码）
         p->key[r - 1] = ls->key.remove ( ls->key.size() - 1 ); //ls的最大关键码转入p
         v->child.insert ( 0, ls->child.remove ( ls->child.size() - 1 ) );
         //同时ls的最右侧孩子过继给v
         if ( v->child[0] ) v->child[0]->parent = v; //作为v的最左侧孩子
         return; //至此，通过右旋已完成当前层（以及所有层）的下溢处理
      }
   } //至此，左兄弟要么为空，要么太“瘦”
// 情况2：向右兄弟借关键码
   if ( p->child.size() - 1 > r ) { //若v不是p的最后一个孩子，则
      BTNodePosi<T> rs = p->child[r + 1]; //右兄弟必存在
      if ( ( _order + 1 ) / 2 < rs->child.size() ) { //若该兄弟足够“胖”，则
         /*DSA*/printf ( " ... case 2\n" );
         v->key.insert ( v->key.size(), p->key[r] ); //p借出一个关键码给v（作为最大关键码）
         p->key[r] = rs->key.remove ( 0 ); //rs的最小关键码转入p
         v->child.insert ( v->child.size(), rs->child.remove ( 0 ) );
         //同时rs的最左侧孩子过继给v
         if ( v->child[v->child.size() - 1] ) //作为v的最右侧孩子
            v->child[v->child.size() - 1]->parent = v;
         return; //至此，通过左旋已完成当前层（以及所有层）的下溢处理
      }
   } //至此，右兄弟要么为空，要么太“瘦”
// 情况3：左、右兄弟要么为空（但不可能同时），要么都太“瘦”——合并
   if ( 0 < r ) { //与左兄弟合并
      /*DSA*/printf ( " ... case 3L\n" );
      BTNodePosi<T> ls = p->child[r - 1]; //左兄弟必存在
      ls->key.insert ( ls->key.size(), p->key.remove ( r - 1 ) ); p->child.remove ( r );
      //p的第r - 1个关键码转入ls，v不再是p的第r个孩子
      ls->child.insert ( ls->child.size(), v->child.remove ( 0 ) );
      if ( ls->child[ls->child.size() - 1] ) //v的最左侧孩子过继给ls做最右侧孩子
         ls->child[ls->child.size() - 1]->parent = ls;
      while ( !v->key.empty() ) { //v剩余的关键码和孩子，依次转入ls
         ls->key.insert ( ls->key.size(), v->key.remove ( 0 ) );
         ls->child.insert ( ls->child.size(), v->child.remove ( 0 ) );
         if ( ls->child[ls->child.size() - 1] ) ls->child[ls->child.size() - 1]->parent = ls;
      }
      release ( v ); //释放v
   } else { //与右兄弟合并
      /*DSA*/printf ( " ... case 3R\n" );
      BTNodePosi<T> rs = p->child[r + 1]; //右兄弟必存在
      rs->key.insert ( 0, p->key.remove ( r ) ); p->child.remove ( r );
      //p的第r个关键码转入rs，v不再是p的第r个孩子
      rs->child.insert ( 0, v->child.remove ( v->child.size() - 1 ) );
      if ( rs->child[0] ) rs->child[0]->parent = rs; //v的最右侧孩子过继给rs做最左侧孩子
      while ( !v->key.empty() ) { //v剩余的关键码和孩子，依次转入rs
         rs->key.insert ( 0, v->key.remove ( v->key.size() - 1 ) );
         rs->child.insert ( 0, v->child.remove ( v->child.size() - 1 ) );
         if ( rs->child[0] ) rs->child[0]->parent = rs;
      }
      release ( v ); //释放v
   }
   solveUnderflow ( p ); //上升一层，如有必要则继续分裂——至多递归O(logn)层
   return;
}
```

## 红黑树

插入

```cpp
/******************************************************************************************
 * RedBlack双红调整算法：解决节点x与其父均为红色的问题。分为两大类情况：
 *    RR-1：2次颜色翻转，2次黑高度更新，1~2次旋转，不再递归
 *    RR-2：3次颜色翻转，3次黑高度更新，0次旋转，需要递归
 ******************************************************************************************/
template <typename T> void RedBlack<T>::solveDoubleRed ( BinNodePosi<T> x ) { //x当前必为红
   if ( IsRoot ( *x ) ) //若已（递归）转至树根，则将其转黑，整树黑高度也随之递增
      {  _root->color = RB_BLACK; _root->height++; return;  } //否则，x的父亲p必存在
   BinNodePosi<T> p = x->parent; if ( IsBlack ( p ) ) return; //若p为黑，则可终止调整。否则
   BinNodePosi<T> g = p->parent; //既然p为红，则x的祖父必存在，且必为黑色
   BinNodePosi<T> u = uncle ( x ); //以下，视x叔父u的颜色分别处理
   if ( IsBlack ( u ) ) { //u为黑色（含NULL）时 //*DSA*/printf("  case RR-1:\n");
      if ( IsLChild ( *x ) == IsLChild ( *p ) ) //若x与p同侧（即zIg-zIg或zAg-zAg），则
         p->color = RB_BLACK; //p由红转黑，x保持红
      else //若x与p异侧（即zIg-zAg或zAg-zIg），则
         x->color = RB_BLACK; //x由红转黑，p保持红
      g->color = RB_RED; //g必定由黑转红
///// 以上虽保证总共两次染色，但因增加了判断而得不偿失
///// 在旋转后将根置黑、孩子置红，虽需三次染色但效率更高
      BinNodePosi<T> gg = g->parent; //曾祖父（great-grand parent）
      BinNodePosi<T> r = FromParentTo ( *g ) = rotateAt ( x ); //调整后的子树根节点
      r->parent = gg; //与原曾祖父联接
   } else { //若u为红色 //*DSA*/printf("  case RR-2:\n");
      p->color = RB_BLACK; p->height++; //p由红转黑
      u->color = RB_BLACK; u->height++; //u由红转黑
      if ( !IsRoot ( *g ) ) g->color = RB_RED; //g若非根，则转红
      solveDoubleRed ( g ); //继续调整g（类似于尾递归，可优化为迭代形式）
   }
}
```

删除

```cpp
/******************************************************************************************
 * RedBlack双黑调整算法：解决节点x与被其替代的节点均为黑色的问题
 * 分为三大类共四种情况：
 *    BB-1 ：2次颜色翻转，2次黑高度更新，1~2次旋转，不再递归
 *    BB-2R：2次颜色翻转，2次黑高度更新，0次旋转，不再递归
 *    BB-2B：1次颜色翻转，1次黑高度更新，0次旋转，需要递归
 *    BB-3 ：2次颜色翻转，2次黑高度更新，1次旋转，转为BB-1或BB2R
 ******************************************************************************************/
template <typename T> void RedBlack<T>::solveDoubleBlack ( BinNodePosi<T> r ) {
   BinNodePosi<T> p = r ? r->parent : _hot; if ( !p ) return; //r的父亲
   BinNodePosi<T> s = ( r == p->lc ) ? p->rc : p->lc; //r的兄弟
   if ( IsBlack ( s ) ) { //兄弟s为黑
      BinNodePosi<T> t = NULL; //s的红孩子（若左、右孩子皆红，左者优先；皆黑时为NULL）
      if ( IsRed ( s->rc ) ) t = s->rc; //右子
      if ( IsRed ( s->lc ) ) t = s->lc; //左子
      if ( t ) { //黑s有红孩子：BB-1
         //*DSA*/printf("  case BB-1: Child ("); print(s->lc); printf(") of BLACK sibling ("); print(s); printf(") is RED\n");
         RBColor oldColor = p->color; //备份原子树根节点p颜色，并对t及其父亲、祖父
      // 以下，通过旋转重平衡，并将新子树的左、右孩子染黑
         BinNodePosi<T> b = FromParentTo ( *p ) = rotateAt ( t ); //旋转
         if ( HasLChild ( *b ) ) { b->lc->color = RB_BLACK; updateHeight ( b->lc ); } //左子
         if ( HasRChild ( *b ) ) { b->rc->color = RB_BLACK; updateHeight ( b->rc ); } //右子
         b->color = oldColor; updateHeight ( b ); //新子树根节点继承原根节点的颜色
         //*DSA*/printBinTree(b, 0, 0);
      } else { //黑s无红孩子
         s->color = RB_RED; s->height--; //s转红
         if ( IsRed ( p ) ) { //BB-2R
            //*DSA*/printf("  case BB-2R: Both children ("); print(s->lc); printf(") and ("); print(s->rc); printf(") of BLACK sibling ("); print(s); printf(") are BLACK, and parent ("); print(p); printf(") is RED\n"); //s孩子均黑，p红
            p->color = RB_BLACK; //p转黑，但黑高度不变
            //*DSA*/printBinTree(p, 0, 0);
         } else { //BB-2B
            //*DSA*/printf("  case BB-2R: Both children ("); print(s->lc); printf(") and ("); print(s->rc); printf(") of BLACK sibling ("); print(s); printf(") are BLACK, and parent ("); print(p); printf(") is BLACK\n"); //s孩子均黑，p黑
            p->height--; //p保持黑，但黑高度下降
            //*DSA*/printBinTree(p, 0, 0);
            solveDoubleBlack ( p ); //递归上溯
         }
      }
   } else { //兄弟s为红：BB-3
      //*DSA*/printf("  case BB-3: sibling ("); print(s); printf(" is RED\n"); //s红（双子俱黑）
      s->color = RB_BLACK; p->color = RB_RED; //s转黑，p转红
      BinNodePosi<T> t = IsLChild ( *s ) ? s->lc : s->rc; //取t与其父s同侧
      _hot = p; FromParentTo ( *p ) = rotateAt ( t ); //对t及其父亲、祖父做平衡调整
      //*DSA*/printBinTree<T>(s, 0, 0);
      solveDoubleBlack ( r ); //继续修正r处双黑——此时的p已转红，故后续只能是BB-1或BB-2R
   }
}
```

## 左式堆

```cpp
template <typename T> //根据相对优先级确定适宜的方式，合并以a和b为根节点的两个左式堆
static BinNodePosi<T> merge ( BinNodePosi<T> a, BinNodePosi<T> b ) {
   if ( ! a ) return b; //退化情况
   if ( ! b ) return a; //退化情况
   if ( lt ( a->data, b->data ) ) swap ( a, b ); //一般情况：首先确保b不大
   ( a->rc = merge ( a->rc, b ) )->parent = a; //将a的右子堆，与b合并
   if ( !a->lc || a->lc->npl < a->rc->npl ) //若有必要
      swap ( a->lc, a->rc ); //交换a的左、右子堆，以确保右子堆的npl不大
   a->npl = a->rc ? a->rc->npl + 1 : 1; //更新a的npl
   return a; //返回合并后的堆顶
} //本算法只实现结构上的合并，堆的规模须由上层调用者负责更新
```

## KMP

主算法

```cpp
int match ( char* P, char* T ) {  //KMP算法
   int* next = buildNext ( P ); //构造next表
   int n = ( int ) strlen ( T ), i = 0; //文本串指针
   int m = ( int ) strlen ( P ), j = 0; //模式串指针
   while ( j < m  && i < n ) //自左向右逐个比对字符
      /*DSA*/{
      /*DSA*/showProgress ( T, P, i - j, j );
      /*DSA*/printNext ( next, i - j, strlen ( P ) );
      /*DSA*/getchar(); printf ( "\n" );
      if ( 0 > j || T[i] == P[j] ) //若匹配，或P已移出最左侧（两个判断的次序不可交换）
         { i ++;  j ++; } //则转到下一字符
      else //否则
         j = next[j]; //模式串右移（注意：文本串不用回退）
      /*DSA*/}
   delete [] next; //释放next表
   return i - j;
}
```

建立`next`表

```cpp
int* buildNext ( char* P ) { //构造模式串P的next表（改进版本）
   size_t m = strlen ( P ), j = 0; //“主”串指针
   int* N = new int[m]; //next表
   int t = N[0] = -1; //模式串指针
   while ( j < m - 1 )
      if ( 0 > t || P[j] == P[t] ) { //匹配
         N[j] = ( P[++j] != P[++t] ? t : N[t] ); //注意此句与未改进之前的区别
      } else //失配
         t = N[t];
   /*DSA*/printString ( P ); printf ( "\n" );
   /*DSA*/printNext ( N, 0, m );
   return N;
}
```

## BM

主算法

```cpp
int match ( char* P, char* T ) { //Boyer-Morre算法（完全版，兼顾Bad Character与Good Suffix）
   int* bc = buildBC ( P ); int* gs = buildGS ( P ); //构造BC表和GS表
   size_t i = 0; //模式串相对于文本串的起始位置（初始时与文本串左对齐）
   while ( strlen ( T ) >= i + strlen ( P ) ) { //不断右移（距离可能不止一个字符）模式串
      int j = strlen ( P ) - 1; //从模式串最末尾的字符开始
      while ( P[j] == T[i + j] ) //自右向左比对
         if ( 0 > --j ) break; /*DSA*/showProgress ( T, P, i, j ); printf ( "\n" ); getchar();
      if ( 0 > j ) //若极大匹配后缀 == 整个模式串（说明已经完全匹配）
         break; //返回匹配位置
      else //否则，适当地移动模式串
         i += max ( gs[j], j - bc[ T[i + j] ] ); //位移量根据BC表和GS表选择大者
   }
   delete [] gs; delete [] bc; //销毁GS表和BC表
   return i;
}
```

bc

```cpp
//*****************************************************************************************
//    0                       bc['X']                                m-1
//    |                       |                                      |
//    ........................X***************************************
//                            .|<------------- 'X' free ------------>|
//*****************************************************************************************
int* buildBC ( char* P ) { //构造Bad Charactor Shift表：O(m + 256)
   int* bc = new int[256]; //BC表，与字符表等长
   for ( size_t j = 0; j < 256; j ++ ) bc[j] = -1; //初始化：首先假设所有字符均未在P中出现
   for ( size_t m = strlen ( P ), j = 0; j < m; j ++ ) //自左向右扫描模式串P
      bc[ P[j] ] = j; //将字符P[j]的BC项更新为j（单调递增）——画家算法
   /*DSA*/printBC ( bc );
   return bc;
}
```

gs

```cpp
int* buildSS ( char* P ) { //构造最大匹配后缀长度表：O(m)
   int m = strlen ( P ); int* ss = new int[m]; //Suffix Size表
   ss[m - 1]  =  m; //对最后一个字符而言，与之匹配的最长后缀就是整个P串
// 以下，从倒数第二个字符起自右向左扫描P，依次计算出ss[]其余各项
   for ( int lo = m - 1, hi = m - 1, j = lo - 1; j >= 0; j -- )
      if ( ( lo < j ) && ( ss[m - hi + j - 1] < j - lo ) ) //情况一
         ss[j] =  ss[m - hi + j - 1]; //直接利用此前已计算出的ss[]
      else { //情况二
         hi = j; lo = min ( lo, hi );
         while ( ( 0 <= lo ) && ( P[lo] == P[m - hi + lo - 1] ) ) //二重循环？
            lo--; //逐个对比处于(lo, hi]前端的字符
         ss[j] = hi - lo;
      }
   /*DSA*/printf ( "-- ss[] Table -------\n" );
   /*DSA*/for ( int i = 0; i < m; i ++ ) printf ( "%4d", i ); printf ( "\n" );
   /*DSA*/printString ( P ); printf ( "\n" );
   /*DSA*/for ( int i = 0; i < m; i ++ ) printf ( "%4d", ss[i] ); printf ( "\n\n" );
   return ss;
}

int* buildGS ( char* P ) { //构造好后缀位移量表：O(m)
   int* ss = buildSS ( P ); //Suffix Size table
   size_t m = strlen ( P ); int* gs = new int[m]; //Good Suffix shift table
   for ( size_t j = 0; j < m; j ++ ) gs[j] = m; //初始化
   for ( size_t i = 0, j = m - 1; j < UINT_MAX; j -- ) //逆向逐一扫描各字符P[j]
      if ( j + 1 == ss[j] ) //若P[0, j] = P[m - j - 1, m)，则
         while ( i < m - j - 1 ) //对于P[m - j - 1]左侧的每个字符P[i]而言（二重循环？）
            gs[i++] = m - j - 1; //m - j - 1都是gs[i]的一种选择
   for ( size_t j = 0; j < m - 1; j ++ ) //画家算法：正向扫描P[]各字符，gs[j]不断递减，直至最小
      gs[m - ss[j] - 1] = m - j - 1; //m - j - 1必是其gs[m - ss[j] - 1]值的一种选择
   /*DSA*/printGS ( P, gs );
   delete [] ss; return gs;
}
```

## Karp-Rabin

```cpp
// 子串指纹快速更新算法
void updateHash ( HashCode& hashT, char* T, size_t m, size_t k, HashCode Dm ) {
   hashT = ( hashT - DIGIT ( T, k - 1 ) * Dm ) % M; //在前一指纹基础上，去除首位T[k - 1]
   hashT = ( hashT * R + DIGIT ( T, k + m - 1 ) ) % M; //添加末位T[k + m - 1]
   if ( 0 > hashT ) hashT += M; //确保散列码落在合法区间内
}
```

## 众数

```cpp
template <typename T> T majEleCandidate ( Vector<T> A ) { //选出具备必要条件的众数候选者
   T maj; //众数候选者
// 线性扫描：借助计数器c，记录maj与其它元素的数量差额
   for ( int c = 0, i = 0; i < A.size(); i++ )
      if ( 0 == c ) { //每当c归零，都意味着此时的前缀P可以剪除
         maj = A[i]; c = 1; //众数候选者改为新的当前元素
      } else //否则
         maj == A[i] ? c++ : c--; //相应地更新差额计数器
   return maj; //至此，原向量的众数若存在，则只能是maj —— 尽管反之不然
}
```

## 中位数

并归有序向量中位数

```cpp
template <typename T> //序列S1[lo1, lo1 + n)和S2[lo2, lo2 + n)分别有序，n > 0，数据项可能重复
T median ( Vector<T>& S1, int lo1, Vector<T>& S2, int lo2, int n ) { //中位数算法（高效版）
   /*DSA*/printf ( "median\n" );
   /*DSA*/for ( int i = 0; i < lo1; i++ ) printf ( "    ." ); for ( int i = 0; i < n; i++ ) print ( S1[lo1+i] ); for ( int i = lo1 + n; i < S1.size(); i++ ) printf ( "    ." ); printf ( "\n" );
   /*DSA*/for ( int i = 0; i < lo2; i++ ) printf ( "    ." ); for ( int i = 0; i < n; i++ ) print ( S2[lo2+i] ); for ( int i = lo2 + n; i < S2.size(); i++ ) printf ( "    ." );  printf ( "\n--\n" );
   if ( n < 3 ) return trivialMedian ( S1, lo1, n, S2, lo2, n ); //递归基
   int mi1 = lo1 + n / 2, mi2 = lo2 + ( n - 1 ) / 2; //长度（接近）减半
   if ( S1[mi1] < S2[mi2] )
      return median ( S1, mi1, S2, lo2, n + lo1 - mi1 ); //取S1右半、S2左半
   else if ( S1[mi1] > S2[mi2] )
      return median ( S1, lo1, S2, mi2, n + lo2 - mi2 ); //取S1左半、S2右半
   else
      return S1[mi1];
}
```

## 快速排序

```cpp
\\partition 简化
template <typename T> //轴点构造算法：通过调整元素位置构造区间[lo, hi)的轴点，并返回其秩
Rank Vector<T>::partition ( Rank lo, Rank hi ) {
    swap ( _elem[lo], _elem[ lo + rand() % ( hi - lo ) ] ); //任选一个元素与首元素交换
    int x = _elem[lo], j = hi;
    // _elem(i, j) <= x < [j, hi)中元素
    for (int i = hi - 1; i >= 0; --i) {
        if (x < _elem[i]) {
            swap(_elem[i], _elem[--j]);
        }
    }
    swap(_elem[j - 1], _elem[lo]);
    return j - 1;
}
```

## shell排序

底层排序应是输入敏感型，如插入排序在已排序列中应从后向前搜索。