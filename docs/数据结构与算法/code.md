# 代码片段

## FFT

```python
def recursive_dtf(a):
    n = len(a)
    if n == 1:
        return a
    a0 = a[0::2]
    a1 = a[1::2]
    w_n = np.exp(2*np.pi*1j/n)
    w = 1
    y = n*[0]
    y0 = recursive_dtf(a0)
    y1 = recursive_dtf(a1)
    for k in range(0 ,int(n/2) ,1):
        y[k] = y0[k]+w*y1[k]
        y[int(n/2)+k] = y0[k]-w*y1[k]
        w = w*w_n
    return y
```

## 打印二叉树

参考：[波兰表示法与表达式树](https://zhuanlan.zhihu.com/p/38013510)

打印一个数据类型为`int`的二叉树，方便调试红黑树

```c++
#ifndef PTREE_H
#define PTREE_H

#include <iostream>

enum Colors {RED, BLACK};

class node {
friend class Tree;
public:
    int data = 0;
    Colors color = Colors::RED;
    node* p = nullptr;
    node* child[2] = {nullptr, nullptr};
    node() = default;
    node(Colors _color, int _data, node* n) : color(_color), data(_data) {
        for (size_t i = 0; i < 2; ++i) {
            child[i] = n;
        }
    }
    explicit node(Colors _color) : node(_color, 0, nullptr) {}

};

class Tree {
public:
    node* const nil = new node(Colors::BLACK);
    node* root = nil;
    Tree() = default;
    Tree(node* n) : nil(n), root(n) {}
    void printTree();
private:
    int maxDepth(const node* n);
    void fillMap(node** map, node* n, int index);
    void putchars(char c, int n);
    void printLeftToParentBranchTop(int w);
    void printRightToParentBranchTop(int w);
    void printLeftToParentBranchBottom(int w);
    void printRightToParentBranchBottom(int w);
    int printNode(node* n, int w);
};

int Tree::maxDepth(const node* n) {
    if (n == nil)
        return 0;
    else {
        int maximum = 0, i, d;
        for (i = 0; i < 2; i++)
            if (maximum < (d = maxDepth(n->child[i])))
                maximum = d;
        return maximum + 1;
    }
}

void Tree::fillMap(node** map, node* n, int index) {
    if (n == nil)
        return;
    int i;

    map[index] = n;
    for (i = 0; i < 2; i++)
       fillMap(map, n->child[i], index * 2 + i + 1);
}

void Tree::putchars(char c, int n) {
    while (n--)
        putchar(c);
}

void Tree::printLeftToParentBranchTop(int w) {
    printf("%*c", w + 1, ' ');
    putchars('_', w - 3);
    printf("/ ");
}

void Tree::printRightToParentBranchTop(int w) {
    putchar('\\');
    putchars('_', w - 3);
    printf("%*c", w + 2, ' ');
}

void Tree::printLeftToParentBranchBottom(int w) {
    printf("%*c%*c", w + 1, '/', w - 1, ' ');
}

void Tree::printRightToParentBranchBottom(int w) {
    printf("%*c%*c", w - 1, '\\', w + 1, ' ');
}

int Tree::printNode(node* n, int w) {
    return printf("%*d %d", w-1, n->data, n->color);
}

void Tree::printTree() {
    int depth = maxDepth(root), i, j, index;
    if (depth == 0) {
        printf("Null tree\n");
        return;
    }
    node** map = (node**)calloc((1 << depth) - 1, sizeof(node*));
    fillMap(map, root, 0);
    for (j = 0, index = 0; j < depth; j++) {
        int w = 1 << (depth - j + 1);
        if (j > 0) {
            // Top part of node to parent branch
            for (i = 0; i < 1 << j; i++)
                if (map[index + i])
                    if (i % 2 == 0) printLeftToParentBranchTop(w);
                    else            printRightToParentBranchTop(w);
                else
                    putchars(' ', w * 2);
            putchar('\n');
            // Bottom part of node to parent branch
            for (i = 0; i < 1 << j; i++)
                if (map[index + i])
                    if (i % 2 == 0) printLeftToParentBranchBottom(w);
                    else            printRightToParentBranchBottom(w);
                else
                    putchars(' ', w * 2);
            putchar('\n');
        }
        // Node content
        for (i = 0; i < 1 << j; i++, index++)
            if (map[index])
                putchars(' ', w * 2 - printNode(map[index], w));
            else
                putchars(' ', w * 2);
        putchar('\n');
    }
    printf("\n");
    free(map);
}
#endif
#endif

```