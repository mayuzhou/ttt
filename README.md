# ttt

import java.util.*;

/**
  数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

  示例 1：
  输入：n = 3
  输出：["((()))","(()())","(())()","()(())","()()()"]

  示例 2：
  输入：n = 1
  输出：["()"]


  提示：
  1 <= n <= 8
  请注意：
  我们将使用程序判题，因此请勿调整给定的代码模版结构，以免误判影响我们对您的评价
  请您将所有答案写在两行 “//======================>” 之间
  **/
public class Ex2 {
    //======================> 下方答案开始

    public List<String> getAllPair(int n) {
        List<String> ret = new ArrayList<>();
        generatePairString(ret, "", n, n);
        return ret;
    }

    public void generatePairString(List<String> ret, String curStr, int l, int r) {
        if (l == 0 && r == 0) {
            ret.add(curStr);
            return;
        }

        if (l > 0) {
            generatePairString(ret,curStr + "(", l - 1, r);
        }
        if (r > l) {
            generatePairString(ret, curStr + ")", l, r - 1);
        }
    }
}


/**

 给你一个整数数组 nums ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
 子数组 是数组中的一个连续部分。

 示例 1：

 输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
 输出：6
 解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。

 示例 2：
 输入：nums = [1]
 输出：1

 示例 3：
 输入：nums = [5,4,-1,7,8]
 输出：23


 提示：
 1 <= nums.length <= 105
 -104 <= nums[i] <= 104

 请注意：
 我们将使用程序判题，因此请勿调整给定的代码模版结构，以免误判影响我们对您的评价
 请您将所有答案写在两行 “//======================>” 之间
 * */
public class Ex3 {
    //======================> 下方答案开始

    public int getMax(int[] a) {
        if (a == null || a.length == 0) {
            return -1;
        }
        int[] d = new int[a.length];
        d[0] = a[0];
        int max = a[0];
        for(int i = 1; i < a.length; i++) {
            d[i] = Math.max(d[i-1]+a[i], a[i]);
            if (d[i] > max) {
                max = d[i];
            }
        }
        return max;
    }
}


import java.util.AbstractList;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 给定一个链表数组，每个链表都已经按升序排列。
 请将所有链表合并到一个升序链表中，返回合并后的链表。

 示例 1：
 输入：lists = [[1,4,5],[1,3,4],[2,6]]
 输出：[1,1,2,3,4,4,5,6]
 解释：链表数组如下：
 [
 1->4->5,
 1->3->4,
 2->6
 ]
 将它们合并到一个有序链表中得到。
 1->1->2->3->4->4->5->6

 示例 2：
 输入：lists = []
 输出：[]

 示例 3：
 输入：lists = [[]]
 输出：[]

 提示：

 k == lists.length
 0 <= k <= 10^4
 0 <= lists[i].length <= 500
 -10^4 <= lists[i][j] <= 10^4
 lists[i] 按 升序 排列
 lists[i].length 的总和不超过 10^4

 请注意：
 我们将使用程序判题，因此请勿调整给定的代码模版结构，以免误判影响我们对您的评价
 请您将所有答案写在两行 “//======================>” 之间
 * */
public class Ex5 {
    //======================> 下方答案开始

    public int[] mergeArray(int[][] lists) {
        if (lists == null || lists.length == 0) {
            return new int[0];
        }

        int total = 0;
        for (int[] l : lists) {
            total += l.length;
        }
        int[] ret = new int[total];
        int[] index = new int[lists.length];

        int retIndex = 0;
        while(true) {
            int curMin = Integer.MAX_VALUE;
            int curIndex = 0;
            for (int i = 0; i < lists.length; i++) {
                if (index[i] != lists[i].length && lists[i][index[i]] < curMin) {
                    curMin = lists[i][index[i]];
                    curIndex = i;
                }
            }
            ret[retIndex] = curMin;
            retIndex++;
            index[curIndex]++;

            boolean breakFlag = false;
            for (int i = 0; i < lists.length; i++) {
                if (index[i] != lists[i].length) {
                    breakFlag = true;
                    break;
                }
            }
            if (breakFlag) {
                break;
            }
        }
        return ret;
    }
}
