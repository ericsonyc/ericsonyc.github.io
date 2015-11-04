---
layout: post
author: Ericson
date: 2015-11-4 20:19
title: Partition List
category: Algorithm
tag: [algorithm,leetcode]
---

Problem:
![Partition List](/public/img/algorithm/partitionlist.jpg)

Solve:<br/>
保存两个指针用来指向链表中小于值的数和大于值的数，然后链接这两个链表，最后返回该链表。<br/>
[Java Code]
{%highlight java%}
public ListNode partition(ListNode head, int x) {
        ListNode little = new ListNode(-2);
        ListNode large = new ListNode(-1);
        ListNode p1 = little;
        ListNode p2 = large;
        while (head != null) {
            if (head.val < x) {
                p1.next = head;
                p1 = p1.next;
            } else {
                p2.next = head;
                p2 = p2.next;
            }
            head = head.next;
        }
        p2.next = null;
        p1.next = large.next;
        return little.next;
    }
{%endhighlight%}
上述代码中little和large来表示小和大的数，然后链接little和large两个链表，最后返回链表头指针。