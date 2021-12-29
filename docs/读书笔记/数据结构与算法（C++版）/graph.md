# 算法图解

## 二分查找

![Screenshot_2021-11-15_17-22-20](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-15_17-22-20.png)

## 图

- 双连通域分解

  ![Screenshot_2021-11-14_14-45-43](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_14-45-43.png)

## BST

- 节点删除
![Screenshot_2021-11-12_17-46-25](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-46-25.png)

## splay tree

- 双层伸展
![Screenshot_2021-11-12_11-08-58](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-08-58.png)
![Screenshot_2021-11-12_11-07-21](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-07-21.png)
![Screenshot_2021-11-12_11-06-39](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-06-39.png)

- 插入
![Screenshot 2021-11-10 122546](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot 2021-11-10 122546.png)

- 删除
![Screenshot 2021-11-10 121622](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot 2021-11-10 121622.png)

## B-树

- 上溢

  ![Screenshot_2021-11-14_14-21-07](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_14-21-07.png)

- 下溢
  - V的左兄弟L存在,且至少包含$\lceil m/2\rceil$ 个关键码
  ![Screenshot_2021-11-12_11-21-35](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-21-35.png)
  - V的右兄弟R存在,且至少包含$\lceil m/2\rceil$个关键码

  ![Screenshot_2021-11-12_11-21-45](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-21-45.png)

  - V的左、右兄弟L和R或者不存在,或者其包含的关键码均不足$\lceil m/2\rceil$个

  ![Screenshot_2021-11-12_11-17-38](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_11-17-38.png)

## 红黑树

- 插入

  - 双红修正（RR-1）

    ![Screenshot_2021-11-12_17-07-26](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-07-26.png)

  - 双红修正（RR-2）

    ![Screenshot_2021-11-12_17-07-46](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-07-46.png)

  - 复杂度

    ![Screenshot_2021-11-12_17-08-04](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-08-04.png)

- 删除

  ![Screenshot_2021-11-12_18-07-52](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_18-07-52.png)

  - 双黑修正（BB-1）

    ![Screenshot_2021-11-12_17-08-25](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-08-25.png)

  - 双黑修正（BB-2-R）

    ![Screenshot_2021-11-12_17-08-35](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-08-35.png)

  - 双黑修正（BB-2-B）

    ![Screenshot_2021-11-12_17-08-48](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-08-48.png)

  - 双黑修正（BB-3）

    ![Screenshot_2021-11-12_17-08-59](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-08-59.png)

  - 双黑修正复杂度

    ![Screenshot_2021-11-12_17-09-10](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-12_17-09-10.png)

## 左式堆

- 合并

  ![Screenshot_2021-11-14_14-53-45](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_14-53-45.png)

## BM

- 坏字符

![Screenshot_2021-11-14_16-34-13](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_16-34-13.png)

- 好后缀

  ![Screenshot_2021-11-14_16-34-41](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_16-34-41.png)
  - ss2gs

    ![Screenshot_2021-11-14_16-35-01](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_16-35-01.png)

  - buildss

    ![Screenshot_2021-11-14_16-35-16](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_16-35-16.png)

- 复杂度

  ![Screenshot_2021-11-14_16-35-40](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-14_16-35-40.png)

## 中位数

并归有序向量中位数

![Screenshot_2021-11-15_17-21-07](https://gitee.com/mostiray/Images_bed/raw/master/notes/dsa/Screenshot_2021-11-15_17-21-07.png)
