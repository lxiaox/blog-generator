---
title: JS排序算法（学习ing）
date: 2018-08-23 11:54:32
tags: （S）排序算法-js
---
不断更新中......

冒泡O(n^2)，选择O(n^2)，插入O(n^2)，快速，计数o(n)，归并，桶排序，基数排序......

### 冒泡排序
+ 基本思想：重复走访要排序的数列，一次比较两个元素，如果这两个数顺序错误就将其交换，每次走访都能找到一个最值，重复走访直到没有要进行交换的元素，那么排序就完成了。
+ 时间复杂度：O(n^2)
+ 冒泡排序过程（升序）：
  1. 比较第一对相邻的元素，如果第一个比第二个大，就交换他们两个。
  2. 按1的方法比较第二对相邻元素，即第二个与第三个，以此类推直到最后一对元素，这时，最后的元素就是最大的数。
  3. 再次重复步骤1、2比较除最后一个数的所有元素。
  4. 如此每次都找到一个当前最大值下次不需在参与比较，直到没有任何一对数字需要比较。
+ JS 代码：

		Array.prototype.bubbleSort = function() {
		    var i, j, temp;
				//每轮比较让最大的冒到最上面，i：轮数=元素个数-1，因为this[0]不需要再比较。
		    for (i = 0; i < this.length - 1; i++)
					//每次选定this[j+1],所以j<this.length-1; 第一轮j+1=this.length-1,第二轮j+1=this.length-2,...所以是要-i
		        for (j = 0; j < this.length - 1 - i; j++)
		            if (this[j] > this[j + 1]) {
		                temp = this[j];
		                this[j] = this[j + 1];
		                this[j + 1] = temp;
		            }
		    return this;
		};
		var num = [2,9,5,8,10,1,32]
		num.bubbleSort()
		console.log(num)	// [1, 2, 5, 8, 9, 10, 32]

### 选择排序
+ 基本思想：首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到所有元素均排序完毕。
+ 时间复杂度：O(n^2)
+ JS 代码：

		Array.prototype.selectionSort = function() {
			var i, j, temp, min
				//每次选出最小的作为this[i]，i：选择的轮数=元素个数-1
			for (i = 0; i < this.length - 1; i++) {
		      	min = i
					//每次从this[i]比较到最后一个：this.length-1；
				for (j = i + 1; j < this.length; j++) {
					if (this[j] < this[min]) {
		              min = j
		            }
		        }
		      temp = this[i]
		      this[i] = this[min]
		      this[min] = temp
		    }			
			return this
		}
		var num = [2,9,5,8,10,1,32]
		num.selectionSort()
		console.log(num)	// [1, 2, 5, 8, 9, 10, 32]

### 插入排序
+ 基本思想：将第一个元素视为已排列元素，取出下一个元素从后向前地与已排列元素进行对比，如果下一个元素（即新元素）比某个元素小，就将这个元素往后移一位，一直比较直到找到小于或等于新元素的，将新元素插到这个元素之后，再重复将多有元素排完。
+ 时间复杂度：O(n^2)
+ JS 代码：

		Array.prototype.insertionSort = function() {
		  var i, j
			//i表示待插入元素，从1开始，因为第一个已插到this[0]
		  for(i = 1; i < this.length; i++) {
		    for(j = 0; j < i; j++){
		      if(this[i] < this[j]){
					//默认j(0~i-1)是已经排好的，this[i]是待插的
					//this[i]<this[j],则把它插入到this[j]的位置
		        this.splice(j,0,this[i])
					//把this[i]插到this[j]之后，原来的this[i]变成了this[i+1]，把它删掉
		        this.splice(i+1,1)
		        break
		      }
		    }
		  }
		  return this
		}
		var num = [2,9,5,8,10,1,32]
		num.insertionSort()
		console.log(num)	// [1, 2, 5, 8, 9, 10, 32]


### 计数排序
+ 基本思想：利用一个新的数组，这个数组的第i项的值就是原数组值为i的个数，然后根据新数组排序。
+ 时间复杂度：O(n+k)；空间:O(n+k)
+ JS 代码：

		Array.prototype.countSort = function() {
		  let C = []
		  for(let i = 0; i < this.length; i++) {
		    C[this[i]] >0 ? C[this[i]] ++ : C[this[i]] = 1
		  }
		  this.splice(0)
		  for(let i = 0; i < C.length; i++) {
		    while(C[i]-- > 0)  this.push(i)
		    
		  }
		  return this
		}
		const arr = [2,9,5,2,4,5,0,8,9,1,3]
		console.log(arr.countSort())



点击[查看排序动画的网站](https://visualgo.net/en)，可以更直观地了解排序的具体过程。