#### 一、基础算法
##### 1.排序
排序，顾名思义，给选中的物体排列顺序，是我们最常用的算法之一。经过长时间的发展，排序的算法有很多很多种，下面让我们逐一来认识一下（所有排序均以升序举例，且数目为n）。  
###### Ⅰ.冒泡排序  
冒泡排序，就像于二图的气泡一样，元素一点一点的根据排序需求移动到指定位置。  
原理：比较两个相邻的元素，将值大的元素交换到右边  
思路：n个数进行n-1趟比较。第一趟比较，先比较第一个数和第二个数，将较大的数放在后面，再比较第二个数和第三个数，将较大的数放在后面，……，如此继续直到比较到最后两个数，将较大的数放在后面，经过第一趟比较，我们将最大的数确定，而且它已将在它应该在的位置上（最大的数已将在最后一位）。第二趟比较，先比较第一个数和第二个数，将较大的放到后面，再比较第二个数和第三个数，将较大的放在后面，……，直到比较到倒数第三个数和倒数第二个数，将较大的放在后面，经过第二趟比较，我们将第二大的数确定，而且它已经在它应该在的位置上（第二大的数在倒数第二位上）。依次类推，经过n-1趟我们就可以将n个数位置都确定。
![avatar](/bubbleSort.gif)

算法分析：n个数要完成排序，总共进行n-1趟排序，第i趟要进行(n-i)次比较，是$O(n^2)$的时间复杂度，而且冒泡排序是稳定的排序。

核心代码：
>for(int i=1;i<n;i++){
&nbsp;&nbsp;&nbsp;&nbsp;for(int j=1;j<=n-i;j++){
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(num[j]>num[j+1]) swap(num[j],num[j+1]);    
&nbsp;&nbsp;&nbsp;&nbsp;}
}

###### Ⅱ.选择排序
选择排序，就像名字一样，选择最大（小）的元素，将其放在指定位置。
原理：进行n-1次选择，每次选择从当前未确定的元素种选择最大（小）的元素，放到指定位置。
思路：首先进行第一次选择，从1下标到n下标中选出最小的数，放在第一位。第二次选择，从2下标到n下标中选出最小的数，放在第二位。第三次选择，从3下标到n下标中选出最小的数，放在第三位。以此类推。
![avatar](/selectionSort.gif)
算法分析：n个数要完成排序，总共进行n-1次选择，第i次要进行(n-i)次比较,是$O(n^2)$的时间复杂度，但是选择排序不是稳定的排序。
核心代码：
>for(int i=1;i<n;i++){
&nbsp;&nbsp;&nbsp;&nbsp;int loc=i;
&nbsp;&nbsp;&nbsp;&nbsp;for(int j=i+1;j<=n;j++){
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(num[j]<num[loc]) loc=j;
&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;swap(num[loc],num[i]);
}

###### Ⅲ.插入排序
插入排序，每次将扫描到的元素插入到它应该在的地方。
原理：构建有序序列，每一次将新的元素插入到已经有序的序列的相应位置上。
思路：将第一待排序序列第一个元素看做一个有序序列，把第二个元素到最后一个元素当成是未排序序列。从头到尾依次扫描未排序序列，将扫描到的每个元素插入有序序列的适当位置。（如果待插入的元素与有序序列中的某个元素相等，则将待插入元素插入到相等元素的后面。）
![avatar](/insertionSort.gif)
算法分析：n个数要完成排序，要进行n-1次扫描，每次都要对该未知元素前面的所有元素进行扫描，是$O(n^2)$的时间复杂度。插入排序是稳定的排序。
核心代码：
>for(int i=2;i<=n;i++){
&nbsp;&nbsp;&nbsp;&nbsp;int now_num=num[i],loc=i;
&nbsp;&nbsp;&nbsp;&nbsp;for(int j=i-1;j>=1;j--){
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(num[j]>now_num){
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;num[j+1]=num[j];
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loc=j;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}else{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;num[loc]=now_num;
}

###### Ⅳ.归并排序
归并排序是建立在归并操作上的一种有效的排序算法。该算法是采用分治法的一个非常典型的应用。
原理：对于每一段需要排序的数列，将其分成两小段，并对这两小段进行排序，用排好序的这两小段生成该段的序列。
思路：分治
![avatar](/merge.png)
再来看看治阶段，我们需要将两个已经有序的子序列合并成一个有序序列，比如上图中的最后一次合并，要将[4,5,7,8]和[1,2,3,6]两个已经有序的子序列，合并为最终序列[1,2,3,4,5,6,7,8]，来看下实现步骤。
![avatar](/merge2.png)
动图示例：
![avatar](/mergeSort.gif)
算法分析：采用分而治之的思维，时间复杂度是$O(nlogn)$。归并排序也是稳定的排序。
核心代码：
>void merge(int ll, int rr) {
&nbsp;&nbsp;&nbsp;&nbsp;  // 用来把 a[ll.. rr - 1] 这一区间的数排序。 t 数组是临时存放有序的版本用的。
&nbsp;&nbsp;&nbsp;&nbsp;  if (rr - ll <= 1) return;
&nbsp;&nbsp;&nbsp;&nbsp;  int mid = ll + (rr - ll >> 1);
&nbsp;&nbsp;&nbsp;&nbsp; merge(ll, mid);
&nbsp;&nbsp;&nbsp;&nbsp;  merge(mid, rr);
&nbsp;&nbsp;&nbsp;&nbsp;  int p = ll, q = mid, s = ll;
&nbsp;&nbsp;&nbsp;&nbsp;  while (s < rr) {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    if (p >= mid || (q < rr && a[p] > a[q])) {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      t[s++] = a[q++];
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      // ans += mid - p;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    } else {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      t[s++] = a[p++];
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  }
&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;for (int i = ll; i < rr; ++i) a[i] = t[i];
}
###### Ⅴ.快速排序
简称快排，是我们在写程序中使用最频繁的排序，有相应的库函数，使用方便。
思路：
1．先从数列中取出一个数作为基准数。
2．分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边。
3．再对左右区间重复第二步，直到各区间只有一个数。
![avatar](/quickSort.gif)
算法分析：也采用了分治的思维，但是与归并不相同，快速排序的时间复杂度的平均期望为$O(nlogn)$，最坏情况为$O(n^2)$，使用Median of Medians 算法的快排为稳定的$O(nlogn)$，但其过于复杂，很少使用。快速排序是不稳定的排序。
核心代码：
>void quicksort(int left, int right) {
&nbsp;&nbsp;&nbsp;&nbsp;	int i, j, t, temp;
&nbsp;&nbsp;&nbsp;&nbsp;	if(left > right)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		return;
&nbsp;&nbsp;&nbsp;&nbsp;    temp = a[left]; //temp中存的就是基准数
&nbsp;&nbsp;&nbsp;&nbsp;    i = left;
&nbsp;&nbsp;&nbsp;&nbsp;    j = right;
&nbsp;&nbsp;&nbsp;&nbsp;    while(i != j) { //顺序很重要，要先从右边开始找
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    	while(a[j] >= temp && i < j)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    		j--;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    	while(a[i] <= temp && i < j)//再找右边的
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    		i++;       
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    	if(i < j){//交换两个数在数组中的位置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    		t = a[i];
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    		a[i] = a[j];
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    		a[j] = t;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    	}
&nbsp;&nbsp;&nbsp;&nbsp;    }
&nbsp;&nbsp;&nbsp;&nbsp;    //最终将基准数归位
&nbsp;&nbsp;&nbsp;&nbsp;    a[left] = a[i];
&nbsp;&nbsp;&nbsp;&nbsp;    a[i] = temp;
&nbsp;&nbsp;&nbsp;&nbsp;    quicksort(left, i-1);//继续处理左边的，这里是一个递归的过程
&nbsp;&nbsp;&nbsp;&nbsp;    quicksort(i+1, right);//继续处理右边的 ，这里是一个递归的过程
}

理解即可，一般在C++中我们使用algorithm下的sort函数就可以了，而且对排序方式的修改也很便捷。
