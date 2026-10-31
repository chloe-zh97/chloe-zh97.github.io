---
title: "时间复杂度和空间复杂度分析"
description: ""
categories: [Algorithm]
tags: [algorithm]
toc: true
math: true
mermaid: false
---

## 问题描述
分组循环判断时间复杂度时，不能简单地用嵌套循环的时间复杂度相乘，需要具体分析分组循环的累加是否等于一个确定值。

### Example 1：分组循环
```java
/**
     * Part 1
     * 假设日志数量是 L，用户数量是 U
     * kᵢ = 第 i 个用户的日志数量
     * 时间复杂度 O(L log L)
     * 空间复杂度 O(U + L)，因为 U <= L, 所以简化为 O(L)
     *  **/
    public static Map<String, Long[]> getUsersMinAndMaxAccessTime(String[][] logs) {
        // userId: access time list
        Map<String, List<Long>> userTimeMap = new HashMap<>();
        // O(L)
        for(String[] log: logs) {
            long time = Long.parseLong(log[0]);
            String userId = log[1], resourceId = log[2];

            userTimeMap.putIfAbsent(userId, new ArrayList<>());
            userTimeMap.get(userId).add(time);
        }

        Map<String, Long[]> ans = new HashMap<>();

        // 外层循环执行 U 次，但是每次排序的 List 长度不同
        for(Map.Entry<String, List<Long>> entry: userTimeMap.entrySet()) {
            String userId = entry.getKey();
            List<Long> list = entry.getValue();
            // sort O(ki log ki), 最坏的情况 O(L log L)
            Collections.sort(list);

            ans.put(userId, new Long[]{list.get(0), list.get(list.size()-1)});
        }

        // print answer
        printMap(ans);

        return ans;
    }
```
- 排序 sort 的复杂度是 O(n log n), 但是在 map 中分组循环，每组的长度是不一样的。每一组的时间复杂度和这个组用户具有的 log 条数相关.


### Example 2: backtracking
回溯中，加入记忆化搜索，对时间复杂度分析的角度可以切换为考虑：
- 一共有多少种状态
- 每种状态做多少种工作

```java
/**
     * Part 2
     * nums[i] 是当前房间 i 的 instruction，表示从当前位置向前跳多少个 room
     * **/
    private static final int INF = Integer.MAX_VALUE / 2;

    public static int getMinInstructionSteps(int[] instructions, int money) {
        int n = instructions.length;
        int[][] memos = new int[n][money+1];
        for(int i=0;i<n;i++)
            Arrays.fill(memos[i], -1);

        int res = backtracking(instructions, 0, money, memos);
        return res >= INF ? -1 : res;
    }

    // 在 nums[i] 这个位置，用 money 到达 9 这个位置最小的跳数
    private static int backtracking(int[] nums, int i, int money, int[][] memos) {
        if(i < 0 || i >= nums.length || money < 0) return INF;
        // 最后一条指令一定是 9
        if(i == nums.length - 1) return 0;

        if(memos[i][money] != -1) return memos[i][money];

        int noPay = backtracking(nums, i+nums[i], money, memos);

        int pay = backtracking(nums, i+nums[i]+1, money-1, memos);
        if(nums[i] > 1) {
            pay = Math.min(pay, backtracking(nums, i+nums[i]-1, money-1, memos));
        }

        int res = Math.min(noPay, pay);
        if(res >= INF) return INF;

        memos[i][money] = res + 1;

        return memos[i][money];
    }
```
```
N：number of rooms
M: money
```
**分析：**
memos 的大小是 N * (M+1), 一共有 N*(M+1) 状态。
对于每一种状态都有以下3种状态, O(3) 常数级别。
- no pay
- 花1$, instruction+1
- 花1$, instruction-1

所以时间复杂度是 O(NM).