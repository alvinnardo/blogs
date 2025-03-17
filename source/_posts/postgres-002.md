---
title: postgres-002
date: 2025-03-17 09:44:39
tags:
---



### execAmi.c

#### 作用

   访问方法接口 (access method interface)



#### 函数调用

- ExecOpenScanR
  
  - 打开一个关系，获取扫描描述
  
  - ExecOpenR
  
  - ExecBeginScan

- ExecOpenR
  
  - 给定一个 oid，返回关系的描述符

- ExecBeginScan
  
  - 在当前的方向开始扫描一个关系，获取扫描描述
  
  - index_beginscan
  
  - heap_beginscan
  
  - ScanDirectionIsBackward

- ExecCloseR
  
  - 关闭扫描描述和关系，如果是索引扫描，则还需关闭索引扫描描述和索引关系
  
  - heap_endscan
  
  - heap_close
  
  - index_endscan
  
  - index_close

- ExecReScan
  
  - 执行 ReScan
  
  - ExecSeqReScan
  
  - ExecIndexReScan
  
  - ExecTeeReScan

- ExecReScanR
  
  - 真正执行 rescan 的地方
  
  - heap_rescan 重新启动一个关系扫描

- ExecMarkPos
  
  - 标记当前扫描的位置
  
  - ExecSeqMarkPos
  
  - ExecIndexMarkPos
  
  - ExecSortMarkPos

- ExecRestrPos
  
  - 恢复之前在 ExecMarkPos() 中保存的扫描位置
  
  - ExecSeqRestrPos
  
  - ExecIndexRestrPos
  
  - ExecSortRestrPos

- ExecCreatR
  
  - 创建一个关系
    
    

### execdebug.h

#### 作用

定义在 executor 中的 debug 行为

在代码中调用了很多宏函数，在该文件中定义这些宏函数被生成具体的函数，或被删除。



### execdefs.h

#### 作用

定义了一些宏



### execFlatten.c (TODO 没看懂)

#### 作用

处理在 SQL 目标列和函数返回之中和 flattening sets 有关的节点



#### 函数调用

- ExecEvalIter
  
  - 每次调用时遍历一次函数所有的返回值类型
  
  - ExecEvalExpr

- ExecEvalFjoin
  
  - ExecEvalIter
  
  - FjoinBumpOuterNodes

- FjoinBumpOuterNodes




