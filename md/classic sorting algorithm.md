[Classic sorting algorithm](https://www.cnblogs.com/onepixel/articles/7674659.html "Top Ten Classical Sorting")
=========================

* Bubble Sort
* selection sort
* insertion sort
* Quick sort
* merge sort
* Hill sort
* Heap sort
* Bucket sort

* Comparison of various sorting algorithms
![Comparison of sorting algorithms](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/sortcompare.png)

#### **Bubble Sort**
* Algorithm overview: compare two adjacent elements, and exchange them if the order is abnormal. After each round of traversal, the last value is the extreme value in the element.
* Animation demo
![Bubble sort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/bubblesort.gif)
* sample code

```C
//Add flag standard bit for simple optimization
int bubblesort(int* array, int len)
{
int i = 0;
int j = 0;
int flag = TRUE;
if(array == NULL)
{
return -1;
}
for(i = 0;i < len -1 && flag; i++)
{
flag = FALSE;
for(j = 0; j <len-1-i;j++)
{
if(array[j] > array[j+1])
{
flag = TRUE;
swap(array+j,array+j+1);
}
}
}
return 0;
}
```
#### **select sort**
* Algorithm overview: first find the extremum in the sequence, put it in the starting position, then find the extremum in the remaining sequence, put it after the sorted sequence, until all the sequences are arranged.
* Animation demo
![Select sort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/selectsort.gif)
* sample code
```C
int selectsort(int* array, int len)
{
int i = 0;
int j = 0;
if(array == NULL)
{
return -1;
}
for(i = 0; i < len -1; i++)
{
int min = i;
for(j = i+1; j < len; j++)
{
if(array[j] < array[min])
{
min = j;
}
}
swap(array+i,array+min);
}
return 0;
}
```
#### **insertion sort**
* Algorithm overview: Insertion sort first constructs an ordered sequence, traverses the unsorted sequence, and inserts them into the ordered sequence one by one in order.
* Animation demo
![Insert sort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/insertsort.gif)
* sample code
```C
int insertsort(int* array, int len)
{
     int i = 0;
     int j = 0;
     if(array == NULL)
     {
         return -1;
     }
     for(i = 0; i < len; i++)
     {
         int pre = i - 1;
         int current = array[i];
         while(pre >= 0 && current < array[pre])
         {
             array[pre+1]=array[pre];
             pre--;
         }
         array[pre+1] = current;
     }
    
}
```
### Hill sort
* Algorithm description: Hill sort is an insertion sort that shrinks increments. For the sequence, the interval is sorted first, and then the interval is continuously reduced until it is 1.
* Animation demo:
![Shellsort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/shellsort.gif)
* sample code
```
int shellsort(int *array, int len)
{
     int gap = 0;
     int i = 0;
     int j = 0;
     for(gap = len / 2;gap > 0;gap /= 2)
     {
         for(i = 0; i < gap; i++)
         {
             for(j = gap + i; j < len; j += gap)
             {
                 int current = array[j];
                 k = j - gap;
                 while(k >= 0 && current < array[k])
                 {
                     array[k+gap] = array[k];
                     k -= gap;
                 }
                 array[k+gap] = current;
             }
         }
     ]
     return 0;
}
```
### Merge sort
* Algorithm description: Merge sort divides the sequence into subsequences continuously, then sorts the subsequences, and finally merges each ordered subsequence into a complete sequence
* Animation demo
![Merge sort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/mergesort.gif)
* sample code
```C
//Merge two sorted sequences
void mergearray(int* a, int first, int mid, int last, int *temp)
{
int k = 0;
int i = first;
int j = mid+1;
while(i <= mid && j <= last)
{
if(a[i] < a[j])
temp[k++] = a[i++];
else
temp[k++] = a[j++];
}
while(i <= mid)
temp[k++] = a[i++];
while(j <= last)
temp[k++] = a[j++];
for(i = 0 ;i < k;i++)
a[first+i] = temp[i];
}

int sort(int *a, int first, int last, int *temp)
{
if(first < last)
{
int mid = (last+first)/2;
sort(a,first,mid,temp);
sort(a,mid+1,last,temp);
mergearray(a,first,mid,last,temp);
}
}

//merge sort
int mergesort(int *array, int len)
{
int temp[len];
sort(array,0,len,temp);
}
```

### Quick Sort
* Algorithm description: quick sort
Quick sort adopts a divide-and-conquer method, taking a reference number, making the left side smaller than it, and the right side larger than it, and the recursive method is repeated to complete the sorting
* Animation demo
![Quick sort](https://github.com/alzhst/Firmware-Engineer-Knowledge/raw/master/Image/quicksort.gif)
* sample code
```C
void qsort(int* array, int first, int last)
{
if(first < last)
{
int i = first;
int j = last;
int temp = array[first];
while(i<j)
{
while(i<j && array[j] > temp)
j--;
if(i<j)
array[i++] = array[j];

while(i<j && array[i] < temp)
i++;
if(i<j)
array[j--] = array[i];
}
array[i] = temp;
qsort(array, first, i-1);
qsort(array,i+1,last);
}
}
//quick sort
void quicksort(int * array, int len)
{
qsort(array,0,len-1);
}
```





