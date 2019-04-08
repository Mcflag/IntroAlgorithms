### 插入排序

插入排序（Insertion Sort）是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

	public static int[] sort(int[] ins) {
        for (int i = 1; i < ins.length; i++) {
            for (int j = i; j > 0; j--) {
                if (ins[j] > ins[j - 1]) {
                    int temp = ins[j];
                    ins[j] = ins[j - 1];
                    ins[j - 1] = temp;
                }
            }
        }
        return ins;
    }

每一次交换都会新创建一个temp，这样造成了浪费，因此可以进行优化，将每个需要交换的值先取出来，再将最后的正确位置空出来，把之前保存的需要插入的数放到正确位置上。

    public static int[] sort2(int[] ins) {
        for (int i = 1; i < ins.length; i++) {
            int temp = ins[i];
            int j;
            for (j = i; j > 0 && ins[j - 1] > temp; j--) {
                ins[j] = ins[j - 1];
            }
            ins[j] = temp;
        }
        return ins;
    }

kotlin版的代码：

	fun sort2(ins: IntArray): IntArray {
	    for (i in 1 until ins.size) {
	        val temp = ins[i]
	        var j: Int = i
	        while (j > 0 && ins[j - 1] > temp) {
	            ins[j] = ins[j - 1]
	            j--
	        }
	        ins[j] = temp
	    }
	    return ins
	}