---
title: postgres 001
date: 2025-03-10 15:15:35
tags:
---



### 文件与作用

- src/backend/main.c
  
  - 程序的入口，选择进入 Postmaster, bootstrap, postgres 模式

- src/backend/include/c.h
  
  - 修改 C 语言中的定义

- src/backend/include/miscadmin.h
  
  - 包含 pg 管理和初始化的定义

- src/backend/include/postgres.h
  
  - 定义 pg 中涉及的类型（如 Oid, bytea, text, name 等）
  
  - msb: most significant bit 最高有效位
    
    

### main.c

#### 作用

程序的入口，选择进入 Postmaster, bootstrap, postgres 模式



#### 函数调用

- init_address_fixup

- PostmasterMain

- BootstrapMain

- PostgresMain



### postgres.c

#### 作用

Postgres 的后端接口



#### 函数调用





### 头文件调用关系

- main
  
  - c.h
  
  - miscadmin.h
    
    - postgres.h
      
      - c.h
    
    - storage/backendid.h
  
  - bootstrap/bootstrap.h
    
    - access/htup.h
      
      - access/attnum.h
        
        - c.h
      
      - storage/bufpage.h
        
        - machine.h
        
        - storage/buf.h
        
        - storage/item.h
          
          - c.h
        
        - storage/itemid.h
        
        - storage/itemptr.h
          
          - c.h
          
          - storage/block.h
            
            - c.h
          
          - storage/off.h
            
            - machine.h
            
            - storage/itemid.h
          
          - storage/itemid.h
      
      - storage/itemptr.h
      
      - utils/nabstime.h
        
        - miscadmin.h
    
    - access/itup.h
      
      - access/ibit.h
        
        - c.h
        
        - utils/memutils.h
          
          - c.h
          
          - utils/bit.h
      
      - access/tupdesc.h
        
        - postgres.h
        
        - access/attnum.h
        
        - nodes/pg_list.h
          
          - c.h
          
          - nodes/nodes.h
            
            - c.h
        
        - catalog/pg_attribute.h
          
          - postgres.h
          
          - access/attnum.h
      
      - storage/itemptr.h
    
    - access/relscan.h
      
      - c.h
      
      - access/skey.h
        
        - postgres.h
        
        - access/attnum.h
      
      - storage/buf.h
      
      - access/htup.h
      
      - storage/itemptr.h
      
      - utils/tqual.h
        
        - postgres.h
        
        - utils/nabstime.h
        
        - access/htup.h
      
      - utils/rel.h
        
        - postgres.h
        
        - storage/fd.h
          
          - c.h
          
          - storage/block.h
        
        - access/strat.h
          
          - postgres.h
          
          - access/attnum.h
          
          - access/skey.h
        
        - access/tupdesc.h
        
        - catalog/pg_am.h
          
          - postgres.h
        
        - catalog/pg_operator.h
          
          - postgres.h
        
        - catalog/pg_class.h
          
          - postgres.h
          
          - utils/nabstime.h
        
        - rewrite/prs2lock.h
          
          - access/attnum.h
          
          - nodes/pg_list.h
    
    - access/skey.h
      
      - postgres.h
      
      - access/attnum.h
    
    - utils/tqual.h
    
    - storage/buf.h
    
    - storage/bufmgr.h
      
      - c.h
      
      - machine.h
      
      - utils/rel.h
      
      - storage/buf_internals.h
        
        - postgres.h
        
        - storage/buf.h
        
        - storage/ipc.h
          
          - c.h
        
        - storage/shmem.h
          
          - storage/spin.h
            
            - ipc.h
              
              - c.h
          
          - utils/hsearch.h
            
            - postgres.h
        
        - miscadmin.h
        
        - storage/lmgr.h
          
          - postgres.h
          
          - storage/itemptr.h
          
          - storage/lock.h
            
            - postgres.h
            
            - storage/itemptr.h
            
            - storage/shmem.h
            
            - storage/spin.h
            
            - storage/backendid.h
            
            - utils/hsearch.h
          
          - utils/rel.h
        
        - utils/rel.h
        
        - utils/relcache.h
          
          - postgres.h
          
          - utils/rel.h
    
    - utils/portal.h
      
      - c.h
      
      - nodes/execnodes.h
        
        - postgres.h
        
        - nodes/nodes.h
        
        - nodes/primnodes.h
          
          - postgres.h
          
          - access/attnum.h
          
          - storage/buf.h
          
          - utils/rel.h
          
          - utils/fcache.h
            
            - fmgr.h
              
              - postgres.h
          
          - nodes/params.h
            
            - postgres.h
            
            - access/attnum.h
          
          - nodes/nodes.h
          
          - nodes/pg_list.h
        
        - nodes/pg_list.h
        
        - nodes/memnodes.h
          
          - c.h
          - utils/memutils.h
          - lib/fstack.h
            - c.h
          - nodes/nodes.h
        
        - storage/item.h
        
        - access/sdir.h
          
          - c.h
        
        - access/htup.h
        
        - access/tupdesc.h
        
        - access/funcindex.h
          
          - postgres.h
        
        - utils/rel.h
        
        - access/relscan.h
        
        - executor/hashjoin.h
          
          - access/htup.h
          
          - storage/ipc.h
        
        - executor/tuptable.h
      
      - nodes/memnodes.h
      
      - nodes/nodes.h
      
      - nodes/pg_list.h
      
      - nodes/plannodes.h
        
        - postgres.h
        
        - nodes/nodes.h
        
        - nodes/pg_list.h
        
        - nodes/primnodes.h
        
        - nodes/execnodes.h
      
      - executor/execdesc.h
        
        - nodes/parsenodes.h
          
          - nodes/nodes.h
          
          - nodes/pg_list.h
          
          - nodes/primnodes.h
          
          - utils/tqual.h
        
        - nodes/plannodes.h
        
        - tcop/desc.h
          
          - catalog/pg_attribute.h
          
          - access/tupdesc.h
    
    - utils/elog.h
    
    - utils/rel.h
  
  - tcop/tcopprot.h
    
    - tcop/dest.h
      
      - catalog/pg_attribute.h
      
      - access/tupdesc.h
    
    - nodes/pg_list.h
    
    - parser/parse_query.h
      
      - nodes/pg_list.h
      
      - nodes/parsenodes.h
      
      - parser/catalog_utils.h
        
        - postgres.h
        
        - access/htup.h
        
        - utils/rel.h
        
        - catalog/pg_proc.h
          
          - postgres.h
          
          - nodes/pg_list.h
          
          - tcop/dest.h
        
        - catalog/pg_type.h
          
          - postgres.h
          
          - utils/rel.h
        
        - utils/syscache.h
          
          - postgres.h
          
          - access/htup.h
          
          - nodes/pg_list.h
      
      - parse_state.h
  
  - port-protos.h
    
    - utils/dynamic_loader.h
